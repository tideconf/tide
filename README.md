# TIDE (Textual Interface for Data Exchange)

![Brenda from Bristol](image.png)

> [!IMPORTANT]  
> This is no more than a hobby project at the moment. I have always been curious about the design and implementation of configuration frameworks, and this is my attempt at creating one. I am not sure if this will ever be used, but I am hoping to learn a bit more about the whole deal of configuration handling. If you are interested in this project, please feel free to contribute or provide feedback. There maybe dragons!

TIDE is a flexible, and type based configuration framework designed to streamline
the way developers handle application configurations. Merging aspects of JSON,
YAML, and TOML, TIDE offers a syntax that prioritizes readability, simplicity,
and robustness. With TIDE, you can define complex configurations, ensuring they
are both human-readable and machine-friendly. TIDE also offers built-in support
for common configuration scenarios like environment variables, secrets, and schema
definitions, making it a useful tool for managing application configurations in
a modern cloud type environment.

## Introduction

### Key Design Goals:

* Readability and Simplicity: Like YAML, but more streamlined to minimize syntactic noise.
* Data Types and Validation: Built-in support for common data types and validation rules.
* Scalability and Performance: Optimized for both small and large configuration files.
* Error Handling and Feedback: More informative error messages and debugging support.
* Security: Designed to prevent common security issues found in JSON and YAMLparsers, by use of strict type checking and validation.

### Syntax and Features:

* Minimalistic Braces: Use a mix of indentation and minimalistic braces to balance between YAML's readability and JSON's structure.
* Type Annotations: Allow explicit type annotations for values to ensure type safety and validation.
* Comments and Documentation: Support both inline and block comments, and special annotations for documenting sections of the configuration.

## Library Support

TIDE is currently supported in the following languages:

* [Go](https://github.com/tideconf/tide-go)
* [Rust](https://github.com/tideconf/tide_rs)

## Examples

### Basic Example

```tide
# This is an inline comment
database {
    type: string = "mysql"
    host: string = "localhost"
    port: integer = 3306
    credentials {
        username: string = "user"
        password: string = "pass"
    }
}

myApp {
    features: array[string] = ["feature1", "feature2", "feature3"]
    numbers: array[integer] = [1, 2, 3]
}
```

## Future Plans

If I ever get around to implementing this, I would like to add the following features:

* Versioning and Backward Compatibility: In-built versioning for configuration schemas to ensure backward compatibility.
* Import Statements: Allow importing configurations from other files to support modularity.
* Environment Variable Integration: Native support for environment variable interpolation.
* Schema Definitions: Introduce schema definitions within the configuration file for self-contained validation rules.
* First-class Function Support: Unlike JSON and TOML, support simple functions or lambda expressions for dynamic configurations.
* Built-in Extensions for Common Use Cases: Provide extensions for common configuration scenarios like database connections, API keys, etc.
