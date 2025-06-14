# DACL: Data And Configuration Language

## Overview

DACL (Data And Configuration Language) is a configuration file format designed for simplicity and robustness, making it easy to read for both humans and machines. Inspired by the conciseness and expressiveness of YAML, DACL eliminates ambiguity and aims for a structure that minimizes errors.

### Design Philosophy

DACL is designed based on the following principles:

- **Simplicity and Robustness:** By limiting features to the essentials and eliminating ambiguity, DACL prevents unexpected errors.
- **Visual Clarity:** A strict 2-space indentation rule makes hierarchical structures immediately apparent.
- **Machine Readability:** Strict syntax and type definitions make parsing easy and integration with applications smooth.
- **Human Readability:** Intuitive and easy-to-understand notation improves maintainability.
- **Modularity:** Importing external files and a powerful reference mechanism promote configuration splitting and reuse.

## Features

DACL offers the following key features:

- **Strict Indentation**
    - Only two spaces are allowed for indentation; tabs are prohibited. Improper indentation results in a parse error.
- **Explicit Data Types**
    - Strings must always be enclosed in double quotes (""). This eliminates ambiguity from type inference.
    - Integers, floating-point numbers, booleans (`true`, `false`), and null values (`null`) are strictly distinguished.
- **Data Structures**
    - Supports maps (key-value pairs) and lists (arrays).
- **Comments**
    - Supports line comments (`#`) for describing configuration content.
- **Powerful Reference Mechanism**
    - References to other values in the configuration file using the form `${path.to.value}`. Referenced values are treated as deep copies for safety.
    - References to environment variables using `${env:VAR_NAME}`. You can also specify a default value with `${env:VAR_NAME:-default_value}`.
    - Import other DACL files under a namespace using `import "file.dacl" as "namespace"`, enabling modular configuration.

### Example DACL File

```
import "database.dacl" as "db" # Import database settings

service:
  name: "my-awesome-app"
  port: ${env:APP_PORT:-8080} # Reference environment variable APP_PORT, default to 8080 if unset

logging:
  level: "info"
  # log_file: "/var/log/${service.name}.log" # Example of internal path reference (commented out)
  log_output:
    - "console"
    - "file"

database_connection:
  type: ${db.type} # Reference from imported db namespace
  host: ${db.host}
  user: ${env:DB_USER} # Required environment variable
  password: "${env:DB_PASSWORD}" # Reference environment variable as string

metrics:
  enabled: true
  interval_seconds: 60

# Example content of database.dacl
# type: "postgresql"
# host: "localhost"
# port: 5432
```

## Development Status

This repository is currently under development. We are working on implementing the DACL parser, validator, and related tools.

## Contributing

Contributions to the DACL project are welcome!
Please participate via GitHub Issues and Pull Requests for bug reports, feature suggestions, and code contributions.
