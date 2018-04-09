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

  <a name="vs-code--plugins"></a><a name="2.1"></a>
  - [2.1](#vs-code--plugins) **Plugins**:
    - Recommended:
      - [Jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest)
      - [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
      - [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
      - [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
    - Optional:
      - [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
      - [Docker](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker)
      - [DotENV](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker)


<a name="vs-code--debugging"></a><a name="2.2"></a>
  - [2.2](#vs-code--debugging) **Debugging**:

    In order to run our **API** with the inspector, use the following debug configuration:

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

    ___

    The easiest way to debug **Jest** tests is to use the [Jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest) plugin. The way it's done at Gojob allows you to run TypeScript tests with the inspector (breakpoints are hit), without having to transpile them to JavaScript nor to build/load their sourcemaps.

    First, create a file `jest-debug.json` in the `.vscode` folder (root of the project). This is basically a copy of our `jest.json` configuration, but with an additional `rootDir` property, and all the options we usually pass through the CLI (`silent`, `notify`, etc). `testRegex` must be able to match all the test files of the project (unit tests, e2e tests, etc).

    ```json
    {
      "rootDir": "../",
      "testRegex": "/(src|e2e)/.*\\.(e2e-test|e2e-spec|test|spec).(ts|tsx|js)$",
      "notify": true,
      "forceExit": true,
      "silent": false,

      // [...]: copy of jest.json
    }
    ```

    > **Note**: This block of properties is the only difference with the original `jest.json`.

    This file will be ignored by `git` as `.vscode` is referenced in `.gitignore`.

    Then, add the following configuration to your VS Code settings:

    ```json
    "jest.autoEnable": false,
    "jest.pathToConfig": ".vscode/jest-debug.json",
    "jest.runAllTestsFirst": false
    ```

    Restart Visual Studio Code and use the **Debug** link above Jest tests. Breakpoints can be used too :tada:

    **NB**: the Jest plugin uses `jest` installed in `./node_modules/jest/bin/jest.js`.

    ![vscode-jest-debug](./assets/vscode-jest-debug.jpg)

    ___

    You don't need the Jest plugin if you want to debug the full execution of tests. Use the following VSCode configuration:

    ```json
    {
      "type": "node",
      "request": "launch",
      "name": "E2E Tests",
      "program": "${workspaceFolder}/node_modules/.bin/jest",
      "args": [
        "--silent=false",
        "--config=${workspaceFolder}/jest.json",
        "--runInBand",
        "--testRegex=/src/.*\\.e2e-test\\.(ts|js)$"
      ],
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
    ```

    *Example for E2E tests. Adapt the parameters depending on the tests you need to run (unit tests, integration tests...). **--runInBand** is mandatory, no matter
    which tests you are running.*

    ___

    To debug **Frontend** projects, use the following configuration:

    ```json
    {
      "type": "chrome",
      "request": "launch",
      "name": "Debug Webapp",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceFolder}/packages/webapp/src",
    }
    ```

    *Example for a "webapp" project, located in a yarn package. Adding `src` to the `webRoot` path is essential with TypeScript code, in order for VSCode to automatically find **sourceMaps**.*



**[⬆ back to top](#table-of-contents)**