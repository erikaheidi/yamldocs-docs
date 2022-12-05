---
title: "Basic Usage"
weight: 2
date: 2022-12-04T10:35:15+01:00
draft: false
---

Yamldocs is built in PHP (cli only) with Minicli. You can run it on a PHP 8.1+ environment or via Docker. Check the [installation]() docs page for details on how to get Yamldocs installed on your system.

## Example YAML

This YAML demonstrates the structure used to define a document and how the markdown is generated:

```yaml
Section1: #structure is based on the actual yaml
  Item1: value0
  Item2: value1
  Item3:
    - value12
    - value13
  Item4: value2

Section2:
  Item1:
    - value12
    - value13
  Item2: value1
  Item3: value3
  Item4: value2

# The document is described in the _meta node, but there are no required fields. Markdown will be generated anyways,
# based on the structure of the YAML document.
_meta:
  # Each node has a description (info) and an array of items that will be presented as a table.
  Section1:
    info: Information about Section 1
    items:
      Item1: The first row
      Item2: The second row

  Section2:
    info: Information about Section 2
    items:
      Item3: The third row
      Item4: The fourth row
    # Setting up a custom example
    example: |
      Section2:
        Item1:
          - value01
          - value02
```

This example file is included in the root of the application folder as `example.yaml`.

## Building one document

Use the `build markdown` command to build a markdown file from a YAML definition. Considering the example YAML from the previous section, this is how you can build it:

```shell
./bin/yamldocs build markdown file=example.yaml output=example.md
```

This command will generate a markdown document based on the `example.yaml` YAML file, saving it to a file called `example.md` on the current directory.

### Generated markdown content

```markdown
    ## example.yaml
    example.yaml YAML reference
    
    
    ## Section1
    Information about Section 1
    
    ### Reference
    
    | Directive | Expects                 |
    |-----------|-------------------------|
    | Item1     | (String) The first row  |
    | Item2     | (String) The second row |
    | Item3     | (Array)                 |
    | Item4     | (String)                |
    
    
    ### Example
    
    ```yaml
    Section1:
      Item1: value0
      Item2: value1
      Item3:
        - value12
        - value13
      Item4: value2
    
    ```
    
    ## Section2
    Information about Section 2
    
    ### Reference
    
    | Directive | Expects                 |
    |-----------|-------------------------|
    | Item1     | (Array)                 |
    | Item2     | (String)                |
    | Item3     | (String) The third row  |
    | Item4     | (String) The fourth row |
    
    
    ### Example
    
    ```yaml
    Section2:
      Item1:
        - value01
        - value02
    ```
```

### Rendered markdown content

## example.yaml
example.yaml YAML reference


## Section1
Information about Section 1

### Reference

| Directive | Expects                 |
|-----------|-------------------------|
| Item1     | (String) The first row  |
| Item2     | (String) The second row |
| Item3     | (Array)                 |
| Item4     | (String)                |


### Example

```yaml
Section1:
  Item1: value0
  Item2: value1
  Item3:
    - value12
    - value13
  Item4: value2

```


## Section2
Information about Section 2

### Reference

| Directive | Expects                 |
|-----------|-------------------------|
| Item1     | (Array)                 |
| Item2     | (String)                |
| Item3     | (String) The third row  |
| Item4     | (String) The fourth row |


### Example

```yaml
Section2:
  Item1:
    - value01
    - value02
```

## Building multiple docs at once

Use the `build docs` command to build markdown docs for all YAML files in a directory:

```shell
./bin/yamldocs build docs source=var/yaml output=var/output
```