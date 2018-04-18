# 命名风格

#### 不要使用缩写

_Bad_

```js
async function readItems() {
  try {
    const res = await axios("...");
  } catch (e) {
    console.log(e.message);
  }
}
```

_Good_

```js
async function readItems() {
  try {
    const response = await axios("...");
  } catch (error) {
    console.log(error.message);
  }
}
```

_常见缩写_

| 全拼     | 缩写       |
| -------- | ---------- |
| response | res        |
| error    | e / err    |
| event    | e / evt    |
| category | cat / cate |

_建议通过 PR 贡献更多的缩写提示_

#### 方法名使用动词开头

#### 变量命名尽可能表述清楚，哪怕会有较长的单词

#### 注意区分复数、单数和不可数名次，该复数的场合尽可能使用复数

#### 常用命名单词

| 描述               | 推荐单词   |
| ------------------ | ---------- |
| 中后台中控         | dashboard  |
| 首页               | homepage   |
| 商品 / 产品 / 货品 | products   |
| 项目               | projects   |
| 案例               | cases      |
| 用户               | users      |
| 个人信息           | profile    |
| 设置               | setting    |
| 分类               | categories |

_建议通过 PR 贡献更多的推荐命名规范_

### 语言要求

* 公共库的开发、注释、git 记录的提交必须使用英文，便于国际化交流；
* 公共库的文档建议以母语中文编写，便于充分表达其含义；
* 项目业务的开发、注释、git 记录采用中文编写，便于中文环境下的快速理解和表达。
