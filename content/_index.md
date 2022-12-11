---
title: "Yamldocs"
weight: 1
date: 2022-12-04T10:35:15+01:00
draft: false
---

Yamldocs is a markdown document generator based on YAML files, written in PHP with [Minicli](https://minicli.dev). It can be used as a standalone app or included as a Composer bin command to be used within existing projects. It is mostly useful to create automated reference docs and comparison tables that can be customized through templates and a common builder interface.

### Use Cases

Here's a few scenarios where Yamldocs can be useful in a project:

- You have a collection of YAML files and would like to bootstrap markdown documentation to describe them
- You want an easier and standardized way to generate comparison or specification tables in markdown
- You want to build an automation to generate docs based in configuration files (YAML)

Check out the [Getting Started Guide](/docs/getting-started/) for more information on how to install and use Yamldocs. Check also the tutorial on [how to create a custom builder to render comparison tables in markdown](/tutorials/creating-comparison-tables/) for a more concrete usage example.