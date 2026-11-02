<div align="center">
  <img src="./GKD.LI.svg" width="100" height="100" alt="GKD Snapshot2Rule">
  <h1>GKD Snapshot2Rule</h1>
</div>

<p align="center">
  <a href="https://raw.githubusercontent.com/teressalodas/GKD-Snapshot2Rule/main/gkd-rule-generator-prompt.md">
    <img src="https://img.shields.io/badge/GitHub-%E8%8E%B7%E5%8F%96%E6%8F%90%E7%A4%BA%E8%AF%8D-red?style=for-the-badge&logo=github" alt="获取提示词" />
  </a>
  <a href="./LICENSE">
    <img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge" alt="License: Apache License 2.0" />
  </a>
</p>

<p align="center">简体中文 | <a href="./README.en.md">English</a></p>

把 GKD 快照的节点树 JSON 直接变成可用的订阅规则。一份结构化提示词，内置选择器语法速查、`fastQuery` 约束和开屏 / 弹窗 / 更新提示等场景模板，让 AI 分析节点树后输出严格 JSON，粘进本地订阅即可生效。

## 用法

1. 悬浮球捕获快照，在快照审查里分享 / 导出，zip 内的节点树 JSON 就是输入。
2. 把 **[提示词](https://raw.githubusercontent.com/teressalodas/GKD-Snapshot2Rule/main/gkd-rule-generator-prompt.md)** 全文 + 快照 JSON 一次发给 AI，温度调到 0。
3. 拿回的规则 JSON 直接粘进 GKD 本地订阅。
4. 不生效时，把失败现象 + 旧规则 + 新快照回喂给 AI 重写（话术见[注意事项](./gkd-rule-notes.md)）。

光发截图不行——AI 拿不到节点属性就写不出可靠选择器，必须用快照 JSON。

## 文件

| 文件 | 用途 |
| ---- | ---- |
| `gkd-rule-generator-prompt.md` | 主提示词，复制全文发给 AI |
| `gkd-rule-locator-appendix.md` | 追加段，目标节点没有 `id`/`vid`/`text`/`desc` 时一起发过去 |
| `gkd-rule-notes.md` | 已知坑、导入注意事项、不生效时的回喂话术 |

## 提示词覆盖

- **选择器语法速查**：属性、比较操作符、关系操作符、属性方法，以及 `@` 锚点和字符串 / 数组的简写形式。
- **fastQuery 约束**：首个属性选择器不满足 `[id=]` / `[vid=]` / `[text=]` 精确匹配时，不会乱开快速查询。
- **场景模板**：开屏广告、有关闭按钮的弹窗、无特征弹窗、更新提示，附上 `matchTime` / `actionMaximum` / `resetMatch` 推荐值。
- **关系定位**：目标节点没有直接特征时走父子 / 兄弟 / 祖先链 / `index` / 弱特征组合，而不是返回空规则。
- **严格 JSON 输出**：只输出规则本体，不带解释和 `` ```json `` 代码块标记，方便直接导入。

## 隐私

- 快照在你的设备上生成，导出为本地 zip，本项目不收集、不上传任何数据。
- 节点树里会带界面上的文字，可能包含账号昵称、手机号、验证码等内容。发给第三方模型前请自行判断可信度，敏感页面建议先删掉无关节点。
- `snapshotUrls` 只是给人看的引用链接，填了不会让规则多发请求，不想要可以删掉这个字段。

## 关于

- AI 生成的规则请一律真机验证后再长期使用：选择器在「当前快照里唯一」不代表在真实界面永远唯一，同一个按钮在不同渲染路径下 `id` 前缀都可能不同。
- 本仓库只是提示词，与 [GKD](https://github.com/gkd-kit/gkd) 官方无关；语法和字段以 [gkd.li](https://gkd.li/guide/) 与 [API 文档](https://gkd.li/api) 为准。
- 发现问题欢迎提交 [Issue](https://github.com/teressalodas/GKD-Snapshot2Rule/issues)，也欢迎 PR / Star。
- 自动点击存在误触风险，涉及资金、隐私、重要操作的页面不要完全依赖规则；请遵守 GKD 及各应用的服务条款。

## 许可证

本项目基于 [Apache License 2.0](./LICENSE) 开源。
