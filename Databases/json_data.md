## JSON Data

- alternative to relation model that is appropriate for semi-structured data
- stands for JavaScript Object Notation 
- standard for "serializing" data objects, usually in files 
- human-readable, useful for data interchange
- **JSON Schema**: JSON Schema is a powerful tool for validating the structure of JSON data
  - constrains things, but can add new properties into data and it is still valid
  - to cancel this behavior, "additionalProperties":false will make it so additional properties are invalid

### Basic constructs (recursive)
- **base values**: number, string, boolean
- **objects**: sets of label-value pairs; enclosed in curly brackets {}
- **arrays**: lists of values; enclosed in straight brackets []

Note: A JSON array is a comma-separated, [] enclosed list of JSON values. Values can be numbers, quoted strings, true, false, null, objects, or arrays. Objects and arrays may be empty. Objects must be a set of label-value pairs.

### Relational Model vs JSON

|                 | Relational   | JSON  | 
|-----------------|--------------|------------|
| Structure       | Tables  | Nested Sets, Arrays  | 
| Schema          | Fixed in advance  | "self-describing" flexible |  
| Queries         | Simple expressive languages  | widely used  |   
| Ordering        | None  | Arrays  |   
| Implementation  | Native systems  | Coupled with Programming Languages. NoSQL Systems  |   

### XML vs JSON
- both good for semi-structured data

|                 | XML   | JSON  | 
|-----------------|--------------|------------|
| Verbosity       | More  | Less  | 
| Complexity          | More  | Less |  
| Validity         | Document type descriptors (DTDs), XML Schema descriptors (XSDs); widely used  | JSON Schema; not widely used  |   
| Prog. Interface        | Clunky, "Impedence Mismatch"  | More direct  |   
| Querying  | XPath, XQuery, XSLT  | JSON Path  | 

- **validity**: ability to specify constraints or restrictions or schema on the structure of data; enforced by tools or by a system

### Syntactically valid JSON
- adheres to basic structural requirements
  - sets of label-value pairs
  - arrays of values
  - base values from predefined types
  
### Semantically valid JSON
- adheres to basical structural requirements + conforms to specified schema
  - JSON file and JSON Schema sent to JSON Validator that checks for syntactic and semantic errors, then sent to JSON Parser 
