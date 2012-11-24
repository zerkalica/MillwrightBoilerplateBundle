MillwrightBoilerplateBundle
=============================

Base html layout and content twig helpers

Inspired by OryzoneBoilerplateBundle(https://github.com/Oryzone/OryzoneBoilerplateBundle)

### Features

* Simple layout html5.html.twig (no hader/footer markup, only body)
* No js and css included
* Twig config variables compatible with OryzoneBoilerplateBundle(https://github.com/Oryzone/OryzoneBoilerplateBundle/blob/master/Resources/doc/index.md#available-variables)
* Some reusable code moved to helpers.html.twig
* Optionaly use ManyMulesModernizrBundle(https://github.com/ManyMules/ManyMulesModernizrBundle) and ManyMulesJQueryBundle(https://github.com/ManyMules/ManyMulesJQueryBundle)

### Installation

``` bash
php composer.phar update zerkalica/millwright-boilerplate-bundle
php composer.phar update manymules/jquery-bundle
php composer.phar update manymules/modernizr-bundle
```

### Add bundle to your application kernel

``` php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new ManyMules\JQueryBundle\ManyMulesJQueryBundle,
        new ManyMules\ModernizrBundle\ManyMulesModernizrBundle,

        new Millwright\BoilerplateBundle\MillwrightBoilerplateBundle,
        // ...
    );
}
```

### Example


```jinjia
{# ::layout.html.twig #}

{% extends 'MillwrightBoilerplateBundle::layout.html.twig' %}
{% import 'MillwrightBoilerplateBundle::helpers.html.twig' as add %}

{% block body_js %}
    {{ add.chromeFrame() }}
    {{ add.googleJs('jquery/1.8.3/jquery.min.js', 'bundles/manymulesjquery/js/jquery.min.js') }}
    {{ add.googleAnalytics(bp_analytics_id|default('')) }}
{% endblock body_js %}

{% block head_js %}
    {{ add.js('bundles/manymulesmodernizr/js/modernizr.min.js' }}
{% endblock head_js %}

{% block favicon %}
    {{ add.favicon('favicon.ico') }}
{% endblock favicon %}

{% block final_css %}
    {{ add.css('twitterbootstrap/responsive.css') }}
{% endblock final_css %}
```

```jinjia
{# view.html.twig #}

{% extends '::layout.html.twig' %}
{% import 'MillwrightBoilerplateBundle::helpers.html.twig' as add %}

{% block body_content %}
    {{ parent() }}
    <div id="app"></div>
{% endblock body_content %}

{% block head_css %}
    {{ parent() }}
    {{ add.css('bundles/myapp/css/main.css') }}
{% endblock head_css %}

{% block body_js %}
    {{ parent() }}
    {{ add.js('bundles/myapp/js/main.app.js') }}
{% endblock body_js %}

{% block body_js_code %}
    {{ parent() }}
    <script>
        {{ add.readyStart() }}
            $('#app').myApp();
        {{ add.readyFinish() }}
    <script>
{% endblock body_js_code %}
```

```yaml
#app/config/config.yml

# Twig Configuration
twig:
    debug:            %kernel.debug%
    strict_variables: %kernel.debug%
    globals:
        bp_language: %locale%
```
