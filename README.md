# Fleex Module Repository

This repository contains a collection of YAML files that define modules for the Fleex tool. These modules can be utilized by the `scan` function in Fleex using the following syntax: 

```bash
fleex scan --params VAR_NAME:var_value
```

## Module Format Example:

```yaml
name: ffuf-module-test
author: xm1k3
description: ffuf module test

vars:
  INPUT: wordlist.txt
  OUTPUT: scan-results.txt
  URL: https://tesla.com/FUZZ

commands:
  - /root/go/bin/ffuf -w {vars.INPUT} -u {vars.URL} -o {vars.OUTPUT} -of csv

```

- name: Unique identifier for the module.
- author: Name of the module creator.
- description: A brief description of the module.

The crucial components are:

- vars: Defines the variables that can be used with assigned default values.
- commands: Specifies the command to be executed. As shown in the example, it can take values from the variables defined in vars.

Note: Each module must contain exactly one INPUT and one OUTPUT variable.