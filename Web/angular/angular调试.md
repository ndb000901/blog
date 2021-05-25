## angular调试

**launch.json**

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch localhost with sourcemaps",
            "type": "chrome",
            "request": "launch",
            "url": "http://localhost:4200",
            "sourceMaps": true,
            "webRoot": "${workspaceRoot}",
            "trace": true,
            "userDataDir": "${workspaceRoot}/.vscode/chrome"
        }
    ]
}
```

**tsconfig.json**

```
{
  "compileOnSave": false,
  "compilerOptions": {
    "outDir": "../dist/", // 注意这个路径
    "rootDir": ".",
    "baseUrl": "src",
    "sourceMap": true, // 这个必须要启用，重要
    "declaration": false,
    "moduleResolution": "node",
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "target": "es5",
    "typeRoots": [
      "node_modules/@types"
    ],
    "lib": [
      "es2016",
      "dom"
    ]
  }
}
```
