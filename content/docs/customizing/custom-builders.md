---
title: "Creating Custom Builders"
weight: 20
date: 2022-12-04T10:35:15+01:00
draft: false
---

To create a custom builder, you must create a class that implements the `BuilderInterface` interface. 

The interface requires two methods to be implemented:

```php
public function configure(array $options = []): void;

public function getMarkdown(Document $document): string;
```

The `configure` method can be used to bootstrap configuration options within the builder upon creation. 

The `getMarkdown` method is where the build should happen; you must return here a string with valid markdown. It will be used as the **content** section of the reference page template.