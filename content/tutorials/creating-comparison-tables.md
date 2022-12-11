---
title: "Creating Comparison Tables"
weight: 20
date: 2022-12-04T10:35:15+01:00
draft: true
---

Given the following YAML source:

```yaml
smb7:
  connection: XLR
  power: via audio interface
  interface: requires audio interface

mv7-k:
  connection: XLR and USB
  power: AAA battery (1x)
  interface: doesn't require use of audio interface (USB)

sm58-lce:
  connection: XLR
  power: AAA battery (1x)
  interface: requires the use of audio interface

```

We'll create a custom builder to generate the following markdown table:

|                | smb7                     | mv7-k                                        | sm58-lce                            |
|----------------|--------------------------|----------------------------------------------|-------------------------------------|
| **connection** | XLR                      | XLR and USB                                  | XLR                                 |
| **power**      | via audio interface      | AAA battery (1x)                             | AAA battery (1x)                    |
| **interface**  | requires audio interface | doesn't require use of audio interface (USB) | requires the use of audio interface |


## Bootstrapping the Application

We'll start by creating a custom Minicli application to hold our custom Yamldocs builds. 

```shell
composer create-project minicli/application mdtables
```

Then, we'll install `yamldocs` as a dev dependency:

```shell
cd mdtables
composer require erikaheidi/yamldocs
```

## Creating a Custom Builder
Next, we'll create a [custom builder](/docs/customizing/custom-builders/) to work on the YAML format we have defined. Create a new class file called `TablesBuilder.php` inside the `app` directory:

```shell
touch app/TablesBuilder.php
```

The following class will iterate through the loaded Yaml that is provided within the `$document` variable and build a markdown table based on its nodes:

```php
<?php

namespace App;

class TablesBuilder implements BuilderInterface
{
    public function configure(array $options = []): void
    {
        //
    }

    /**
     * @param Document $document
     * @return string
     */
    public function getMarkdown(Document $document): string
    {
        $headers[] = "";
        $rows = [];
        $items = [];

        //normalize data structure
        foreach ($document->yaml as $key => $specs) {
            $headers[] = $key;
            foreach ($specs as $name => $spec) {
                $items[$name][$key] = $spec;
            }
        }

        //prepare table rows
        foreach ($items as $spec => $nodes) {
            $specRow[] = "**$spec**";
            foreach ($nodes as $name => $spec) {
                $specRow[] = $spec;
            }
            $rows[] = $specRow;
            $specRow = [];
        }

        //return rendered table in markdown
        return Mark::table($rows, $headers);
    }

}

```

Copy this code to your own class file and save it.

Next, you'll need to include the custom builder within Yamldocs configuration. Create a new `yamldocs.yaml` file in the root of the app:

```shell
touch yamldocs.yaml
```

Open it in your code editor and include the following:

```yaml
builders:
  tables: App\TablesBuilder
```

## Testing the Custom Builder

Save and close the file. Now you can test it with the YAML presented at the beginning of this tutorial:

```yaml
smb7:
  connection: XLR
  power: via audio interface
  interface: requires audio interface

mv7-k:
  connection: XLR and USB
  power: AAA battery (1x)
  interface: doesn't require use of audio interface (USB)

sm58-lce:
  connection: XLR
  power: AAA battery (1x)
  interface: requires the use of audio interface

```

Save this file as `shure-mics.yaml` in your app's root. Then, run `yamldocs` with:

```shell
./vendor/bin/yamldocs build markdown file=shure-mics.yaml output=shure-mics.md builder=tables
```

The generated markdown file should look like this:

```markdown
|                | smb7                     | mv7-k                                        | sm58-lce                            |
|----------------|--------------------------|----------------------------------------------|-------------------------------------|
| **connection** | XLR                      | XLR and USB                                  | XLR                                 |
| **power**      | via audio interface      | AAA battery (1x)                             | AAA battery (1x)                    |
| **interface**  | requires audio interface | doesn't require use of audio interface (USB) | requires the use of audio interface |

```