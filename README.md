# Gojob TypeScript Style Guide() {

*A mostly reasonable approach to TypeScript*

## Table of Contents

  1. [Naming Conventions](#naming-conventions)

## Naming Conventions

  <a name="naming-conventions--interfaces"></a><a name="1.1"></a>
  - [1.1](#naming-conventions--interfaces) **Interfaces**: Use "I" as a prefix for interface names.

  ```typescript
      // bad
      interface User {
          name: string;
      }

      // good
      interface IUser {
          name: string;
      }
  ```

  <a name="naming-conventions--types"></a><a name="1.2"></a>
    - [1.2](#naming-conventions--types) **Types**: Use PascalCase for type names.

  <a name="naming-conventions--enum-values"></a><a name="1.3"></a>
    - [1.3](#naming-conventions--enum-values) **Enum values**: Use PascalCase for enum values.

  <a name="naming-conventions--functions"></a><a name="1.4"></a>
    - [1.4](#naming-conventions--functions) **Functions**: Use camelCase for function names.

  <a name="naming-conventions--property-local-var"></a><a name="1.5"></a>
    - [1.5](#naming-conventions--property-local-var) **Property names and local variables**: Use camelCase for property names and local variables.

  <a name="naming-conventions--private-properties"></a><a name="1.6"></a>
    - [1.6](#naming-conventions--private-properties) **Private properties**: Do not use a prefix for private properties name (not even `_`).

  <a name="naming-conventions--whole-words"></a><a name="1.7"></a>
    - [1.7](#naming-conventions--whole-words) **Whole words**: Use whole words in names when possible.


**[⬆ back to top](#table-of-contents)**


**Tools**

  - Code Style Linters
    - [TSLint](https://palantir.github.io/tslint/)
    - [Gojob Style tslint-base.json](https://github.com/gojob-1337/typescript/blob/master/package/tslint-config-gojob/tslint-base.json)

**Blogs**

  - [Gojob tech](https://tech.gojob.com/)

**[⬆ back to top](#table-of-contents)**

# };