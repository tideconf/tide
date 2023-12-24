# TIDE (Textual Interface for Data Exchange)

![Brenda from Bristol](image.png)

> [!IMPORTANT]  
> This is no more than a hobby project at the moment. I have always been curious about the design and implementation of configuration frameworks, and this is my attempt at creating one. I am not sure if this will ever be used, but I am hoping to learn a bit more about the whole deal of configuration handling. If you are interested in this project, please feel free to contribute or provide feedback.

TIDE is a flexible, and type based configuration framework designed to streamline the way developers handle application configurations. Merging aspects of JSON, YAML, and TOML, TIDE offers a syntax that prioritizes readability, simplicity, and robustness. With TIDE, you can define complex configurations, ensuring they are both human-readable and machine-friendly. TIDE also offers built-in support for common configuration scenarios like environment variables, secrets, and schema definitions, making it a useful tool for managing application configurations in a modern cloud type environment.

## Introduction

### Key Design Goals:

* Readability and Simplicity: Like YAML, but more streamlined to minimize syntactic noise.
* Data Types and Validation: Built-in support for common data types and validation rules.
* Scalability and Performance: Optimized for both small and large configuration files.
* Extensibility and Interoperability: Easy integration with various programming languages and environments.
* Error Handling and Feedback: More informative error messages and debugging support.
* Versioning and Backward Compatibility: In-built versioning for configuration schemas to ensure backward compatibility.
* Security: Designed to prevent common security issues found in JSON and YAML parsers.

### Syntax and Features:

* Minimalistic Braces: Use a mix of indentation and minimalistic braces to balance between YAML's readability and JSON's structure.
* Type Annotations: Allow explicit type annotations for values to ensure type safety and validation.
* Comments and Documentation: Support both inline and block comments, and special annotations for documenting sections of the configuration.
* Import Statements: Allow importing configurations from other files to support modularity.
* Environment Variable Integration: Native support for environment variable interpolation.
* Schema Definitions: Introduce schema definitions within the configuration file for self-contained validation rules.
* First-class Function Support: Unlike JSON and TOML, support simple functions or lambda expressions for dynamic configurations.
* Built-in Extensions for Common Use Cases: Provide extensions for common configuration scenarios like database connections, API keys, etc.

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
```

### Advanced Configuration with Function and Import

```tide
import "common_settings.tide"

server {
    host: string = "0.0.0.0"
    port: integer = env("SERVER_PORT") | default(8080)
    calculate_max_connections: lambda = (type, users) => if type == "large" then users * 2 else users
    max_connections: integer = calculate_max_connections("medium", 100)
}

logging {
    level: string = "info"
    format: string = "[$timestamp] $level: $message"
    timestamp: lambda = () => now().format("yyyy-MM-dd HH:mm:ss")
}
```

### Configuration with Schema Definition

```tide
schema AppConfig {
    version: string
    debug: boolean
    features: array[string]
}

config AppConfig {
    version: string = "1.0.0"
    debug: boolean = false
    features: array[string] = ["feature1", "feature2", "feature3"]
}
```

### Configuration with Built-in Extension
    
```tide
api {
    key: string = secret("api_key")
    base_url: string = "https://api.example.com"
    timeout: integer = 30
}

# Built-in extension for handling secrets
secret "api_key" {
    source: string = "environment"
    fallback: string = "default_key"
}
```

## Library Support

TIDE is currently supported in the following languages:

* [Go](https://github.com/tideconf/tide-go)