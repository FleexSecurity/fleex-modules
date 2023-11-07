
# Fleex modules Repository

This repository contains a collection of YAML files that define modules for the Fleex tool. These modules can be utilized by the `scan` function in Fleex using the following syntax: 

```bash
fleex scan --module testmodule.yaml --params VAR_NAME:var_value
```

## Module Format Example:

```yaml
# testmodule.yaml

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

- `name`: Unique identifier for the module.
- `author`: Name of the module creator.
- `description`: A brief description of the module.

The crucial components are:

- `vars`: Defines the variables that can be used with assigned default values.
- `commands`: Specifies the command to be executed. As shown in the example, it can take values from the variables defined in `vars`.

**Note**: Each module must contain exactly one `INPUT` and one `OUTPUT` variable.

## Usage

1 - Clone this repository.
2- Navigate to the directory containing the module you want to use.
3- Run the Fleex tool with the desired parameters.

Example Usage:

```bash
fleex scan --module testmodule.yaml
  --params INPUT:new_wordlist.txt
  --params OUTPUT:new_scan_results.txt
  --params URL:https://example.com/FUZZ
```

This repository is a first version and may be expanded in the future to support multiple commands per module.

## Contributing:

If you would like to contribute to this repository, feel free to fork and create a pull request with your changes. Make sure to follow the same format as existing modules.

**Note**: This is an initial version of the repository and may be subject to future updates and improvements.

## License
Fleex modules is distributed under Apache-2.0 License
