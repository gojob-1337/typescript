# tslint-config-gojob

This package provides Gojob's base TS `tslint-base.json` (without React plugins) as an extensible shared config.

## Usage

We export one TSLint configurations for your usage.

### tslint-config-gojob

Our default export contains all of our TSLint rules, including `tslint:recommended`. It requires `tslint`.

1. Install the correct versions of each package, which are listed by the command:

  ```sh
  yarn add @gojob/tslint-config --dev
  ```
  
2. Within your `tsconfig.json` add the following extends:

  ```json
  {
    "extends": "tslint-config-gojob/tslint-base"
  }
  ```
