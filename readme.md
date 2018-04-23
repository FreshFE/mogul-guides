# Mogul

Mogul (_['moɡl]_) 是针对食行生鲜中后台业务特别定制的相关开发规范和工具。使用 React、MobX、Ant Design 等工具实现，在此要感谢 Ant Design 提供了优秀的组件库。

Mogul 提供如下内容：

1.  在 Ant Design 基础上的交互规范，以 Axure 为参考；
1.  代码和命名推荐指南；
1.  Mogul CLI 工具；
1.  快速开始的文件结构；
1.  再度封装的业务组件；
1.  最佳实践指南。

## 第一步：创建文件目录

```bash
$ yarn global add mogul-cli
$ mogul new
 ? type project name please: startapp
```

## 第二步：探索文件目录

```bash
# @todo 添加 rewired
startapp                                   # 生成的文件根目录
  |- src                                   # 业务代码目录
      |- index.js                          # 入口文件
      |- pages                             # Tip: pages 目录下的一级文件夹以首字母大写驼峰法为准
          |- App                           # App 路由一级入口
              |- index.js
          |- Dashboard                     # Dashboard 路由二级入口
              |- index.js
              |- store.js                  # Dashboard 的局部状态（包含 menu 等数据的维护）
          |- Sign                          # Sign 路由二级入口
              |- index.js
          |- Homepage                      # Homepage 路由三级入口
              |- index.js
      |- utils                             # 工具方法目录
          |- axios.js                      # 封装 axios，处理通用错误
          |- env.js                        # 封装环境变量，统一引用
          |- token.js                      # 封装 token 存储函数
  |- package.json
  |- README.md                             # 项目安装、部署及文档入口
  |- yarn.lock
  |- .eslintrc                             # 仅作用于编辑器的 eslint 设置
  |- .prittierrc                           # 提交的代码必须通过 prittier 调整
  |- .gitignore
```

## 第三步：探索 package.json

```json
{
  "name": "startapp",
  "version": "0.0.1",
  "private": false,
  "license": "MIT",
  "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "module": "plop module"
  },
  "devDependencies": {
    "mogul": "^0.0.8"
  }
}
```

## 第四步：命令行快速创建

```bash
# 切换至 startapp 根目录
$ yarn module
```

```bash
pages
  |- App
  |- Dashboard
  |- Sign
  |- Homepage
  |- Projects
      |- index.js                # 入口文件
      |- Collection.js           # 数据集展示
      |- Query.js                # 查询条件
      |- Editor.js               # 新建和更新页
      |- Detail.js               # 详情页
      |- style.module.css        # 样式文件
      |- services
          |- api.js              # 接口
          |- pagination.js       # 分页 MobX
          |- query.js            # 查询 MobX
          |- collection.js       # 数据集 MobX
      |- __test__                # 测试文件目录
```

建议为一个实体(Entity)数据新建一个 module，如果是 Project 实体下关联的子实体，如 Project Category，则新建 module：

```bash
$ yarn module
 ? type module name please: ProjectCategory
```

```bash
pages
  |- App
  |- Dashboard
  |- Sign
  |- Homepage
  |- Sign
  |- Projects
  |- ProjectCategories
```

## 第五步：了解路由的运作机制

Mogul Router 通过 React Router 实现了路由业务，在 Mogul 和 React Router 哲学里，一切皆组件。

### 路由树结构与项目目录结构的对应关系

`路由结构图`

```bash
                                           # 对应的目录文件
/                                          # pages/App/index.js
  |- /dashboard                            # pages/Dashboard/index.js
      |- /dashboard/projects               # pages/Projects/index.js
          |- /dashboard/projects/:id       # pages/Projects/Collection.js
          |- /dashboard/projects/:id/edit  # pages/Projects/Editor.js
      |- /dashboard/project-categories     # pages/ProjectCategories/index.js
  |- /sign                                 # pages/Sign/index.js
      |- /sign/in                          # pages/Sign/In.js
      |- /sign/up                          # pages/Sign/Up.js
```

`目录结构图`

```bash
pages
  |- App
      |- index.js
  |- Dashboard
      |- index.js
  |- Projects
      |- index.js
      |- Collection.js
      |- Detail.js
      |- 更多完整目录查看第二步
  |- ProjectCategories
  |- Sign
```

### 路由代码

`src/pages/App/index.js`

```js
import { App } from "@mogul/components";
import { Route, Switch } from "react-router";
import Dashboard from "./Dashboard.js";
import Sign from "./Sign.js";

export default ({ match }) => (
  <App>
    <Switch>
      <Route path={match.url + "/dashboard"} component={Dashboard} />
      <Route path={match.url + "/sign"} component={Sign} />
    </Switch>
  </App>
);
```

`src/pages/Dashboard/index.js`

```js
import { Dashboard } from "@mogul/components";
import { Route, Switch } from "react-router";
import Projects from "./Projects.js";
import ProjectCategories from "./ProjectCategories.js";
import store from "./store.js";

export default ({ match }) => (
  <Dashboard store={store}>
    <Switch>
      <Route path={match.url + "/projects"} component={Projects} />
      <Route
        path={match.url + "/project-categories"}
        component={ProjectCategories}
      />
      {/* 由 @mogul/cli 插入新的 module */}
    </Switch>
  </Dashboard>
);
```

`src/pages/Projects/index.js`

```js
import { Route, Switch } from "react-router";
import Collection from "./Collection.js";
import Detail from "./Detail.js";

export default ({ match }) => (
  <Switch>
    <Route path={match.url} component={Collection} exact />
    <Route path={match.url + "/:id"} component={Detail} />
  </Switch>
);
```

## 进一步阅读

* [@mogul/cli 的接口文档](cli.md)
* [类库](libraries.md)
* 掌握常用的 Mogul router 和相关的 Params、QueryString 处理
* 基于 MobX 的状态管理
* 常见的范式布局
* [通用的命名规范](rules.md)
* 嵌套关联实体的 CURD 最佳实践

## 相关资料

* [React 中文文档](https://doc.react-china.org)
* [MobX 中文文档](http://cn.mobx.js.org)
* [Ant Design 组件文档](https://ant.design/docs/react/introduce-cn)
