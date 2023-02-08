# yarrrml-json-schema

A JSON Schema to let code editors (e.g., VS Code) syntax-check YARRRML files.

> YARRRML (pronounced /jɑɹməl/) is a human readable text-based representation for declarative generation rules.
> It is a subset of \[YAML\], a widely used data serialization language designed to be human-friendly.

- [YARRRML](https://rml.io/yarrrml/spec/)
- [VS Code support for JSON schema](https://code.visualstudio.com/docs/languages/json)
- [VS Code support of JSON schemas for YAML files](https://github.com/redhat-developer/vscode-yaml#associating-schemas)

## Usage

There are two ways to use this JSON Schema:

- Add to Visual Studio Code's `settings.json`:

  ```json
    "yaml.schemas": {
    	"https://rdmr.eu/yarrrml-json-schema/yarrrml-json-schema.json": "*.rml.yaml"
    }
  ```

- Add to the top of a YAML file:

  ```yaml
  # yaml-language-server: $schema=https://rdmr.eu/yarrrml-json-schema/yarrrml-json-schema.json
  ```

## Contributing

1. Format your code with `prettier` (`npm format`).
1. Check if your additions improve the reporting in your editor.
1. Check if no extra validation errors occur (`npm test`).
