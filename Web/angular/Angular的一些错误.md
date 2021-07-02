# Angular的一些错误

**1.环境**

```
# ng version

Angular CLI: 11.2.12
Node: 15.13.0
OS: linux x64

Angular: 11.2.13
... animations, common, compiler, compiler-cli, core, forms
... localize, platform-browser, platform-browser-dynamic, router
Ivy Workspace: Yes

Package                         Version
---------------------------------------------------------
@angular-devkit/architect       0.1102.12
@angular-devkit/build-angular   0.1102.12
@angular-devkit/core            11.2.12
@angular-devkit/schematics      11.2.12
@angular/cdk                    9.2.4
@angular/cli                    11.2.12
@schematics/angular             11.0.1
@schematics/update              0.1102.12
rxjs                            6.6.7
typescript                      4.1.5


```

## 错误1

```
Cannot find module '@schematics/angular/utility/config'
Require stack:
- /home/hello/myCode/web/angular/hero/node_modules/angular-bootstrap-md/schematics/ng-add/mdb-setup.js
- /home/hello/myCode/web/angular/hero/node_modules/@angular-devkit/schematics/tools/export-ref.js
- /home/hello/myCode/web/angular/hero/node_modules/@angular-devkit/schematics/tools/index.js
- /home/hello/myCode/web/angular/hero/node_modules/@angular/cli/utilities/json-schema.js
- /home/hello/myCode/web/angular/hero/node_modules/@angular/cli/models/command-runner.js
- /home/hello/myCode/web/angular/hero/node_modules/@angular/cli/lib/cli/index.js
- /usr/local/node/node-v15.13.0-linux-x64/lib/node_modules/@angular/cli/lib/init.js
- /usr/local/node/node-v15.13.0-linux-x64/lib/node_modules/@angular/cli/bin/ng

```

**解决**

```
sudo npm i @schematics/angular@11.0.1
```


## 错误2 NullInjectorError: No provider for NzMessageService!

**解决**

```
import { NzMessageModule } from 'ng-zorro-antd/message';
```
