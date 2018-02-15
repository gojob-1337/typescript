# Gojob IDE tips and configurations

*Some tips and configurations on most popular IDE.*

## Table of Contents

  1. [WebStorm](#webstorm)
  2. [Visual Studio Code](#visual-studio-code)

## WebStorm
  > **Note**: This assumes you are currently using [WebStorm](https://www.jetbrains.com/webstorm/) IDE.

  <a name="webstorm--file-watcher"></a><a name="1.1"></a>
  - [1.1](#webstorm--file-watcher) **File watcher**: Allow the IDE to reformat the code depending on `tslint.json`,after any file modification.
    > **Note**: This configuration assumes you use the TypeScript language and the [TSLint](https://palantir.github.io/tslint/) linter.

    Go to `Tools -> File Watchers`, configure a new watcher doing as follows:
    ```text
      File Type = TypeScript
      Scope = Project Files
      Program = <binary of tslint package within node_modules>
      Arguments = -c $ProjectFileDir$/tslint.json --fix $FileName$
      Working directory = $FileDir$
    ```
    ![Autolint](./assets/autolint.png)

## Visual Studio Code
  > **Note**: This assumes you are currently using [Visual Studio Code](https://code.visualstudio.com/).

  <a name="vs-code--plugins"></a><a name="1.1"></a>
  - [1.1](#vs-code--plugins) **Plugins**:
    - Recommended:
      - [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
      - [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
      - [Jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest)
      - [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
    - Optional:
      - [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
      - [Docker](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker)
      - [DotENV](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker)


<a name="vs-code--debugging"></a><a name="1.2"></a>
  - [1.2](#vs-code--debugging) **Debugging**:

    In order to run our API with the inspector, use the following debug configuration:
    ```json
    {
      "type": "node",
      "request": "launch",
      "name": "Run the API",
      "program": "${workspaceRoot}/index.js",
      "restart": true,
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
    ```

    > **Note**: Node v8+ is required in order to use the (new) inspector.

    You can now put breakpoints in the TypeScript code of the project and use the debugger of VS Code.


**[⬆ back to top](#table-of-contents)**