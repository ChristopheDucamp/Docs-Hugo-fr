---
title: Alternatives de Modélisation
linktitle: Langages Alternatifs de Modélisation
description: En plus des modèles Go, Hugo supporte la modélisation puissante d'Ace de @yosssi et la modélisation Amber de @eknkc.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [templates, modèles]
#tags: [amber,ace,templating languages]
menu:
  docs:
    parent: "Templates"
    weight: 170
weight: 170
sections_weight: 170
draft: false
aliases: [/templates/ace/,/templates/amber/]
toc: true
---

## Modèles Ace

Pour la documentation du modèle suivez les liens à partir du  [projet Ace](https://github.com/yosssi/ace).

* Ace templates must be named with the ace-suffix; e.g., `list.ace`
* It's possible to use both Go templates and Ace templates side by side and even include one into the other
* Full Go template syntax support, including all the useful helper [template functions][]
* Partials can be included both with the Ace and the Go template syntax. For example, the following two will have the same output in Ace:
    * `= include partials/foo.html .`
    * `{{ partial "foo" . }}`

One noticeable difference between Ace and the other templating engines in Hugo is [Ace's inheritance support through base and inner templates][aceinheritance].

In Hugo, the Ace base template will be chosen with the same rule set as for [Go base templates][].

```bash
.:
index.ace

./blog:
single.ace
baseof.ace

./_default:
baseof.ace  list.ace  single.ace  single-baseof.ace
```

{{% note %}}
Note that the `html` suffix is needed even if the filename is suffixed `ace`. This does not work from inside a theme ([issue #763](https://github.com/gohugoio/hugo/issues/763)).
{{% /note %}}

Some examples for the layout files above:

* Home page: `./index.ace` +  `./_default/baseof.ace`
* Single page in the `blog` section: `./blog/single.ace` +  `./blog/baseof.ace`
* Single page in another section: `./_default/single.ace` +  `./_default/single-baseof.ace`
* Taxonomy page in any section: `./_default/list.ace` +  `./_default/baseof.ace`

{{% note %}}
In most cases, one `baseof.ace` in `_default` will suffice. An Ace template without a reference to a base section (e.g., `= content`) will be handled as a standalone template.
{{% /note %}}

## Modèles Amber

Pour la documentation des modèles Amber, suivez les liens à partir du [projet Amber][].

* Amber templates must be named with the Amber suffix; e.g., `list.amber`
* Partials in Amber or HTML can be included with the Amber template syntax:
    * `import ../partials/test.html `
    * `import ../partials/test_a.amber `

[aceinheritance]: https://github.com/yosssi/ace/tree/master/examples/base_inner_template
[projet Amber]: https://github.com/eknkc/amber
[template functions]: /fonctions/
[Go templates]: /templates/introduction/
[Go base templates]: /templates/base/