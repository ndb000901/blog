## Access to XMLHttpRequest at 'http://127.0.0.1/data.json' from origin 'http://localhost:4200' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.

**创建proxy.conf.json**

```
{
    "/api": {
      "target": "https://api.spotify.com/v1",
      "secure": true,
      "changeOrigin": true,
      "pathRewrite": {
        "^/api": ""
      }
    }
  }
```

**修改angular.json**

```
"serve": {
          "builder": "@angular-devkit/build-angular:dev-server",
          "options": {
            "browserTarget": "projectname:build",
            "proxyConfig": "./proxy.conf.json"
          },
```
