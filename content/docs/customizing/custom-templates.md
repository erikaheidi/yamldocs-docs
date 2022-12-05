---
title: "Working with Templates"
weight: 1
date: 2022-12-04T10:35:15+01:00
draft: false
---

Yamldocs works by default with [Stencil]() templates, a simple templating library that is often used to bootstrap files and has no external dependencies.

There are two templates included within the application's `/templates` folder:

- reference_page.tpl
- reference_page_section.tpl

These templates are used by the `DefaultBuilder` to build the final markdown through the built-in build commands. If you want to customize the templates, you need to overwrite them. Set the templates in a folder inside your app and set up a `templatesDir` parameter on your `yamldocs.php` [configuration](/docs/getting-started/configuration-options/).
It's worth noting that the use of templates is not mandatory when creating custom builders.

The `reference_page.tpl` is the parent template that renders the final markdown page result. For instance, if you need to include a front-matter to your markdown, this is most probably the place where it should go.

The `reference_page_section.tpl` is a sub-template used to render each section of the generated page.

Here's the content of each file for reference:

#### reference_page.tpl
```markdown
    ## {{ title }}
    {{ description }}
    
    {{ content }}
```

#### reference_page_section.tpl
```markdown
    ## {{ item }}
    {{ description }}
    
    ### Reference
    
    {{ reference_table }}
    
    ### Example
    
    ```yaml
    {{ example }}
    ```
    
    {{ notes }}
```

These variables are passed at build time, and some are obtained from the source YAML. Both the `example` and `notes` (optional) placeholders are expected to be defined as metadata fields in the source YAML.

## Generating content for Hugo websites

To generate content for a Hugo website, you'll want to overwrite the default `reference_page.tpl` to include a front-matter section.

What goes on the front-matter often depends on the theme and layouts used, which can have custom variables. A simple example would be:

```markdown
    ---
    title: "{{ title }}"
    description: "{{ description }}"
    weight: 1
    ---

    {{ description }}
    
    {{ content }}
```
