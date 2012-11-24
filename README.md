MillwrightBoilerplateBundle
=============================

Base html layout and content twig helpers

Inspired by OryzoneBoilerplateBundle(https://github.com/Oryzone/OryzoneBoilerplateBundle)

Features
--------

* Simple layout html5.html.twig (no hader/footer markup, only body, js, css parts)
* Twig config variables compatible with OryzoneBoilerplateBundle(https://github.com/Oryzone/OryzoneBoilerplateBundle/blob/master/Resources/doc/index.md#available-variables)
* Some reusable code moved to helpers.html.twig

Example
-------

```jinjia
{# ::layout.html.twig #}

{% extends 'MillwrightBoilerplateBundle::layout.html.twig' %}
{% import 'MillwrightBoilerplateBundle::helpers.html.twig' as add %}

{% block body_js %}
    {{ add.chromeFrame() }}
    {{ add.googleJs('jquery/1.8.2/jquery.min.js', 'bundles/millwrightboilerplate/js/jquery-1.8.2.min.js') }}
    {{ add.googleAnalytics(bp_analytics_id|default('')) }}
{% endblock body_js %}

{% block head_js %}
    {{ add.js('bundles/millwrightboilerplate/js/modernizr-2.6.2.min.js' }}
{% endblock head_js %}

{% block favicon %}
    {{ add.favicon('bundles/millwrightboilerplate/favicon.ico') }}
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
