# .js 专项规则

`.js` 文件适用全部通用覆盖规则，唯一差别是注释格式：

- 用 **JSDoc** 替代 TSDoc。
- `.js` 没有类型系统兜底，类型标注必须写全在 JSDoc 里：`@param {string} name`、`@returns {Promise<User[]>}`。
