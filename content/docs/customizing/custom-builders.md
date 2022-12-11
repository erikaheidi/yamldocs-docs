---
title: "Creating Custom Builders"
weight: 20
date: 2022-12-04T10:35:15+01:00
draft: false
---

Creating a custom builder is useful when you have a fixed YAML structure and you want to obtain more polished results, enriching data or focusing on specific nodes from the source files.

To create a custom builder, you must create a class that implements the `BuilderInterface` interface. 

The interface requires two methods to be implemented:

```php
public function configure(array $options = []): void;

public function getMarkdown(Document $document): string;
```

The `configure` method can be used to bootstrap configuration options within the builder upon creation. 

The `getMarkdown` method is where the build should happen; you must return here a string. It will be used as the **content** section of the reference page template.

The `TestBuilder` is a simple example that can be used as template:

```php
<?php

namespace Builders;

use App\BuilderInterface;
use App\Document;

class TestBuilder implements BuilderInterface
{
    public function configure(array $options = []): void
    {
        //
    }

    public function getMarkdown(Document $document): string
    {
        return "test";
    }
}

```

Once you have your custom builder, you need to set it up in a `yamldocs.yaml` configuration file in the root of your application:

```yaml
builders:
  default: Builders\DefaultBuilder
  test: App\TestBuilder
```

Check also our tutorial on [how to create a custom builder to render comparison tables in markdown](/tutorials/creating-comparison-tables/).