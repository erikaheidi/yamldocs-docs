---
title: "Configuration Options"
weight: 40
date: 2022-12-04T10:35:15+01:00
draft: false
---

To overwrite default settings, you can create a `yamldocs.yaml` config file in the root of your application, where you have Yamldocs set up as a dependency.

Currently, there are three main settings:

- `debug`: (boolean) default is set to true.
- `templatesDir`: (string) default is set to the source Yamldocs folder. You can replace this with your own directory containing custom templates.
- `builders`: (array) expects an array that sets an identifier as key and the path to a valid cals implementing the BuilderInterface. The identifier is used to select this builder when running `yamldocs build`.

## Example 1: Setting up Templates Folder

```yaml
templatesDir: templates
```

## Example 2: Setting up Custom Builders

```yaml
builders:
  - default: Builders\DefaultBuilder
  - custom: App\MyCustomBuilder
```