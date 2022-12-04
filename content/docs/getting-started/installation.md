---
title: "Installation"
weight: 1
# geekdocFlatSection: false
geekdocToc: 6
geekdocHidden: false
date: 2022-12-04T10:35:15+01:00
draft: false
---

{{< toc format=html >}}

Yamldocs is a versatile markdown generator that can be installed and used in different ways, depending on how much customization you need.

## Requirements

To install and execute Yamldocs, you'll need the following:

- a PHP 8.1+ cli environment with the following extensions:
  - php-xml
- Composer

## Installing Yamldocs as part of an existing PHP application
This is the recommended method to use Yamldocs. It will give you more customization options, such as creating custom markdown builders that are specific to each type of YAML you have in your project.

Because it is unlikely that you need to generate docs in production, it is generally a better approach to install Yamldocs as a **dev** requirement:
```shell
composer require-dev erikaheidi/yamldocs
```

This will make available the `./vendor/bin/yamldocs` executable that you can call directly from your application root folder.

## Creating a Yamldocs application
If you can't include Yamldocs in your main application, or you just want to keep Yamldocs as a separate project for automating your docs (with GitHub Actions, for instance), you can bootstrap a placeholder app with Minicli:

```shell
composer create-project minicli/application my-super-docs
```
This will create a barebones Minicli application (cli-only) where you can set up your custom templates and builders. It gives the same benefits as the previous method, but keeps everything separate from your main application - also useful when your main application is not written in PHP.

Then you can proceed with the recommended installation method, which includes Yamldocs as a dependency:

```shell
composer require erikaheidi/yamldocs
```

## Installing Yamldocs as standalone app
If you prefer to install Yamldocs locally as a standalone application, you'll need PHP 8.1+ and Composer. Then, clone this repository and install dependencies:

```shell
git clone https://github.com/erikaheidi/yamldocs.git
cd yamldocs
composer install
```

Then you'll be able to run `yamldocs` like this:

```shell
./bin/yamldocs build markdown file=example.yaml output=example.md
```
