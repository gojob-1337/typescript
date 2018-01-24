# Gojob IDE tips and configurations

*Some tips and configurations on most popular IDE.*

## Table of Contents

  1. [WebStorm](#webstorm)

## WebStorm
  > **Note**: This assumes your are currently use [WebStorm](https://www.jetbrains.com/webstorm/) IDE.

  <a name="webstorm--file-watcher"></a><a name="1.1"></a>
  - [1.1](#webstorm--file-watcher) **File watcher**: Allow to the IDE to reformat code depends on `tslint.json` after modifications on file.
    > **Note**: This configuration assumes your are on TypeScript language and use [TSLint](https://palantir.github.io/tslint/) linter.
   
    Go to `Tools->File Watchers`, add a new one and as the picture below, fill the following fields:
    ```text
      File Type = TypeScript
      Scope = Project Files
      Program = <binary of tslint package within node_modules>
      Arguments = -c $ProjectFileDir$/tslint.json --fix $FileName$
      Working directory = $FileDir$
    ```
    ![Autolint](./assets/autolint.png)
  

**[⬆ back to top](#table-of-contents)**