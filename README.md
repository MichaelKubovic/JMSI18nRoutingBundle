This is fork of JMSI18nRoutingBundle
====================

This repo is forked version of [JMSI18nRoutingBundle](https://github.com/schmittjoh/JMSI18nRoutingBundle).

The main aim is to add support for scenario where multiple hosts can have multiple languages. The following urls are all handled by single action.

```
domain.com/english-slug
domain.com/de/deutsch-slug
domain.de/deutsch-slug
domain.de/en/english-slug
```

It's highly recommended to use ```canonical``` element or other mechasnism to avoid panalties for duplicate contents. See [Multi-regional and multilingual sites](https://support.google.com/webmasters/answer/182192#3).

Internally the bundle expands routes similarly to how original author does, expect that it generates separate routes for every configured host. Routes are then matched by sf2 router by looking at the host attribute.

The bundle has been testes with the following routing configuration:

```yaml
my_bundle:
    resource: "@MyBundle/Resources/config/routing.yml"
    prefix:   /
    host:     "{domain}"
    requirements:
        domain: domain.com|domain.de
    defaults:
        domain: "domain.com"
```

The following configuration must be used to achieve desired behaviour. Locale defined in hostmap sets default language for that host.

```yaml
jms_i18n_routing:
    default_locale: 'sk'
    locales: ['sk', 'en', 'de']
    strategy: prefix_except_default
    hosts:
        sk: domain.sk
        en: domain.com
        de: domain.de
    redirect_to_host: false
```


This bundle is not backward-compatible and default strategies probably won't work as expected.
