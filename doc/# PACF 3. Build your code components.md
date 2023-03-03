# PACF 3. Build your code components

After you finish code Build It!

```CLI
npm run build
```

## 构建文件解析

该构建在 LinearInputControl/generated 文件夹下生成更新的 TypeScript 类型声明文件。 该组件被编译到 out/controls/LinearInputControl 文件夹中。 构建工件包括：

* bundle.js – Bundled component source code.
* ControlManifest.xml – Actual component manifest file that is uploaded to the Microsoft Dataverse organization.

### eslint

eslint 规则可能会影响您的构建，具体取决于它们的配置方式。 如果您在构建期间收到错误：

```Shell
[12:00:00 PM] [build]  Failed:
[pcf-1065] [Error] ESLint validation error:
 10:26  error  'EventListenerOrEventListenerObject' is not defined  no-undef
```

1. 检查 .eslintrc.json 中的 eslint 规则并将 linting 规则设置为 ["warn"]。 例如，如果您收到错误：
2. 错误“EventListenerOrEventListenerObject”未定义 no-undef
3. 然后你可以打开 .eslintrc.json 并编辑规则，为规则 no-undef 添加一个 ["warn"] 值：

```JSON
"rules": {
      "no-unused-vars": "off",
      "no-undef": ["warn"]
    }
```
