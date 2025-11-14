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

## Remarks

- Shortcut keys (e.g., `m`, `po`, `iv`) validate, but are not suggested in VS Code.
- Supports:
  - Base specification [YARRRML](https://w3id.org/yarrrml/spec/)
  - Extension [HTTP Request Access](https://rml.io/yarrrml/spec/access/httprequest/)
  - Extension [Dynamic Targets](https://rml.io/yarrrml/spec/target/dynamictarget/)
  - Extension [Incremental RML generation using YARRRML (LDES)](https://rml.io/yarrrml/spec/incrml/)

## Contributing

1. Format your code with `prettier` (`npm format`).
1. Check if your additions improve the reporting in your editor.
1. Check if no extra validation errors occur (`npm test`).

### Code conventions

- Smurfs1N: either a single Smurf or an array of Smurfs (oneOf/[$ref, items])
- SmurfOpt: either an object or some inline value for Smurf (oneOf/[SmurfObj, SmurfAbbr])
- SmurfObj: Smurf as an object
- SmurfAbbr: Smurf as an inlined value

```json
  "Subject1N": {
    "oneOf": [
      { "$ref": "#/definitions/SubjectOpt" },
      { "type": "array", "items": { "$ref": "#/definitions/SubjectOpt" } }
    ]
  },
  "SubjectOpt": {
    "oneOf": [
      { "$ref": "#/definitions/SubjectAbbr" },
      { "$ref": "#/definitions/SubjectObj" }
    ]
  },
  "SubjectAbbr": { "type": "string" },
  "SubjectObj": {
    "type": "object",
    "properties": {
      "value": { "type": "string" },
      "targets": { "$ref": "#/definitions/Targets1N" }
    },
    "patternProperties": {
      "^(t|target)$": { "$ref": "#/definitions/SubjectCx/properties/targets" },
      "^(v)$": { "$ref": "#/definitions/SubjectCx/properties/value" }
    }
  }
```
