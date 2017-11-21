# How to run and debug flow a script in node using babel

Currently Node.js support may ES6 features but full support for modules (`import` and `export`) is still missing.
Similarly Node.js can't directly execute Flow type-annotated scripts. Standard solution is transpilation to node accepted
form of Javascript. In case one wants to avoid this intermediate step, `babel-node` is a solution.

[`babel-node`][1] allows transparent in-memory transpilation and interpretation of Javascript using node. It allows both
launching a script file and REPL mode. (Authors warn it's not for production use.)

To run flow annotated ES6 module install required npm packages (it may be installed globally as well):

```
npm install babel-cli babel-preset-env babel-preset-flow
```

Run script using:

```
node_modules/.bin/babel-node --presets env,flow script.js
```

## Debugging in babel-node

`babel-node` works with `--inspect-brk` option eventhough it is not mentioned on its web or in output of help.

1. Run

   ```
   node_modules/.bin/babel-node --inspect-brk --presets env,flow script.js
   ```

2. Use any node debugging UI. In case of *Visual Studio Code*:
   1. Open debug panel (Menu > View > Debug)
   2. Make sure attaching configuration is present.  
      Debug configurations (Menu > Debug > Open Configurations) should contain a configuration like
      
      ```
      {
          "type": "node",
          "request": "attach",
          "name": "Attach by Process ID",
          "processId": "${command:PickProcess}"
      }
      ```
   
   3. Select the attaching configuration, start debugging (Menu > Debug > Start Debugging), select `babel-node` process.

[1]: https://babeljs.io/docs/usage/cli/#babel-node

