# Mogul

针对食行生鲜业务特别定制的中后台开发规范和相关工具。使用 React、MobX、Ant Design 等工具组织，在此要感谢 Ant Design 提供了优秀的组件库。

Mogul 提供如下内容：

1.  在 Ant Design 基础上的交互规范，以 Axure 为参考；
1.  代码和命名推荐指南；
1.  Mogul CLI 工具；
1.  快速开始的文件结构；
1.  再度封装的业务组件；
1.  最佳实践指南。

## 第一步：创建文件目录

```bash
$ npm install --global @mogul/cli
$ mogul new startapp
$ cd startapp
$ yarn start
```

## 第二步：探索文件目录

```bash
# @todo 添加 rewired
startapp                                   # 生成的文件根目录
  |- src                                   # 业务代码目录
      |- index.js                          # 入口文件
      |- pages                             # Tip: pages 目录下的一级文件夹以首字母大写驼峰法为准
          |- Layouts
              |- Dashboard.js
          |- Homepage
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
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^16.2.0",
    "react-dom": "^16.2.0",
    "react-scripts": "1.1.1"
    // @todo 替换成 react-scripts-rewired
    // @todo 添加 pittier git commit 钩子
    // @todo 添加 @mogul/box 控制 react、react-dom、ant-design 等版本
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom"
  }
}
```

## 第四步：命令行快速创建

```bash
# 切换至 startapp 根目录
# 创建名为 project 的 module
$ mogul module project
```

```bash
pages
  |- Layouts
  |- Homepage
  |- Project
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

建议为一个实体数据新建一个 module，如果是 Project 实体下关联的子实体，如 Project Category，则新建 module：

```bash
$ mogul module ProjectCategory
```

```bash
pages
  |- Layouts
  |- Homepage
  |- Project
  |- ProjectCategory
```

## 相关资料

* [React 中文文档](https://doc.react-china.org)
* [MobX 中文文档](http://cn.mobx.js.org)
* [Ant Design 组件文档](https://ant.design/docs/react/introduce-cn)
