---
layout: post
title:  "Symfony2 ile Widget Yapısı"
date:  2015-08-30 
categories: symfony2 widget
---

Elimden geldiğince yaptığım sistemlerin görünen kısımlarında (frontend) elemanları parçalamaya çabalarım. Widget olarak adlandırmayı 
tercih ediyorum bu kısımları. Önceleri Symfony ile yaptığım projelerde twig dosyalarımda her parçayı render içinde controller çağırarak
aşağıdaki şekilde parçalayarak, çakma bir widget yapısı oluşturuyordum.


{% highlight ruby %}
  {% raw %} {{ render(controller('AddmeanAdvertBundle:Default:index', {place: "widget_docket_top"})) }}{% endraw %}
{% endhighlight %} 


Fakat bu durumda, performansı yerlere çekebiliyordum. Kendimce farklı bir yöntem oluşturmaya karar verdim. Widget olacak kısımları ayrı birer 
servis olarak yazarsam daha performanslı olacağını, daha doğru bir yaklaşım olabileceğini düşündüm.

Uyguladığım yöntem ise, adımsal olarak şöyleydi;

 - Bir baseWidget abstract class`ımda tüm ortak işleri görüp, mecburi metodları belirledim.
 - SiteBundle`ım içerisinde bir Widget klasörü açıp içerisine, her widget için bir sınıf oluşturup baseWidget sınıfımdan extend ederek gerekli ayarları yaptım.
 - Bu widget`ları birer servis olarak tanımladım.
 - Widget servislerimi twig içerisinde kullanabilecek bir twig extension yazdım.
 - Tüm widgetları gerekli yerlere yerleştirdim.

Gereksiz hiç bir yük olmadan widget`larıma ulaşıp onları çalıştırabiliyorum artık. Kod örneklerine bakarak daha iyi anlayabileceğinizi düşünüyorum.

#### BaseWidget Sınıfım

{% highlight php %}
<?php


namespace Addmean\MainBundle\Widget;


use Addmean\UserBundle\Manager\GroupManager;
use Doctrine\ORM\EntityManager;

abstract class Base
{
    /**
     * @var \Twig_Environment
     */
    protected $twig;
    /**
     * @var EntityManager
     */
    protected $em;

    /**
     * @var array
     */
    protected $data;

    /** @var  GroupManager */
    protected $gm;
    /**
     * @param EntityManager $em
     * @param \Twig_Environment $twig
     * @param GroupManager $gm
     */
    public function __construct(EntityManager $em, \Twig_Environment $twig,GroupManager $gm)
    {
        $this->em = $em;
        $this->twig = $twig;
        $this->gm = $gm;
    }

    /**
     * Rendered view
     * @return string
     */
    public function render()
    {
        return $this->twig->render($this->getView(), $this->getData());
    }

    /**
     * Twig file
     * @return string
     */
    abstract public function getView();

    /**
     * Data for passing twig file
     * @return array
     */
    public function getData()
    {
        return $this->data;
    }

    /**
     * @param array $data
     * @return void
     */
    abstract public function setData(array $data);
}
{% endhighlight %}

#### Örnek Widget Sınıfım

{% highlight php %}
<?php

namespace SiteBundle\Widget;


use Addmean\MainBundle\Widget\Base;

class RecentNews extends Base
{
    /**
     * @inheritDoc
     */
    public function getView()
    {
        return "SiteBundle:Widget\\RecentNews:view.html.twig";
    }

    /**
     * @inheritDoc
     */
    public function setData(array $data)
    {
        $group = $this->gm->get($data['group']);

        $newsRepo = $this->em->getRepository('AddmeanNewsBundle:News');
        $news = $newsRepo->findBy(['group'=>$group,'published'=>true],['id'=>'desc'],$data['limit']);
        $data['items'] = $news;
        $data['group'] = $group;
        $this->data = $data;
        return $this;
    }
}
{% endhighlight %}

#### Servis Tanımlama Örneğim 

{% highlight yaml %}
services:
    widget.recent_news:
    class: SiteBundle\Widget\RecentNews
    arguments: ["@doctrine.orm.entity_manager","@twig","@addmean_group_manager"]
{% endhighlight %} 

#### Twig Extension Örneği

{% highlight php %}
<?php


namespace Addmean\MainBundle\Twig;

use Addmean\MainBundle\Widget\Base;
use Symfony\Component\DependencyInjection\ContainerInterface;


/**
 * Class WidgetExtension
 * @package Addmean\MainBundle\Twig
 */
class WidgetExtension extends \Twig_Extension
{
    /**
     * @var ContainerInterface
     */
    private $container;

    public function __construct(ContainerInterface $container)
    {
        $this->container = $container;
    }

    /**
     * @return array
     */
    public function getFilters()
    {
        return [];
    }

    /**
     * @return array
     */
    public function getFunctions()
    {
        return [
            new \Twig_SimpleFunction('widget', [$this, 'getWidget'],['is_safe'=>['html']])
        ];
    }

    public function getWidget($name,$data=[])
    {
        /** @var Base $widget */
        $widget = $this->container->get('widget.' . $name);
        $widget->setData($data);
        return $widget->render();
    }

    /**
     * @inheritDoc
     */
    public function getName()
    {
        return "widget_extension";
    }

}
{% endhighlight %}

#### Ve sonunda kullandım

{% highlight ruby %}
{% raw %}{{ widget('recent_news',{group: app.request.get('group'),limit: 5}) }}{% endraw %}
{% endhighlight %}

