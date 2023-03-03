# PACF 6. React controls & platform libraries

您可以使用 React 和平台库实现显着的性能提升。 当您使用 React 和平台库时，您使用的是 Power Apps 平台使用的相同基础结构。 这意味着您不再需要为每个控件单独打包 React 和 Fluent 库。 所有控件将共享一个公共库实例和版本，以提供无缝和一致的体验。

通过重新使用现有平台的 React 和 Fluent 库，您可以获得以下好处：

1. 减少控制包大小
2. 优化的解决方案包装
3. 更快的运行时传输、脚本和控制渲染
4. 凭借重新使用这些组件资源所带来的好处，我们预计在该功能全面上市后，这种方法将成为创建所有 Power Apps 代码组件的首选方式。

## Create a React component

There is a new --framework (-fw) parameter for the pac pcf init command. Set the value of this parameter to react.
The following table shows the long form of the commands:
Parameter Value
--name ReactSample
--namespace SampleNamespace
--template field
--framework react
--run-npm-install true (default)
The following PowerShell command uses the parameter shortcuts and will create a React component project and run npm-install in the folder where you run the command:

```CLI
pac pcf init -n ReactSample -ns SampleNamespace -t field -fw react -npm
```

You can now build and view the control in the test harness as usual using npm start.

After you build the control you can package it inside solutions and use it for model-driven apps (including custom pages) and canvas apps like standard code components.

## Sample

Ref: <https://github.com/microsoft/PowerApps-Samples/tree/master/component-framework/ChoicesPickerReactControl>
PowerApps-Samples/component-framework/ChoicesPickerReactControl at master · microsoft/PowerApps-Samples (github.com)

## Differences from standard components

### ControlManifest.Input.xml

!!!The control element control-type attribute is set to virtual rather than standard.

***Changing this value does not convert a component from one type to another. （一定用命令新建，不要改standard的组件，没用）***

Within the resources element, you will find two new platform-library element child elements like the following:

```XML
<resources>
    <code path="index.ts" order="1" />
   <platform-library name="React" version="16.8.6" />
   <platform-library name="Fluent" version="8.29.0" />
</resources>
```

#### Fluent

Fluent 是 Microsoft 设计的一套全新的用户界面设计语言，旨在提供一致的、现代化的体验，适用于各种 Microsoft 产品和服务。它强调简单、现代和无缝的体验，包括流畅的动画、漂亮的图标、清晰的排版和简单的控件。Fluent 还提供了一些简单、通用的设计原则和指南，帮助开发者在自己的应用程序中实现 Fluent 的风格和体验。Fluent 设计语言的风格非常适合用于 Microsoft Power Apps 组件框架的开发。

### Index.ts

The ReactControl.init method for control initialization does not have div parameters because these controls do not render the DOM directly. Instead ReactControl.updateView returns a ReactElement which has the details of the actual control in React format.

### bundle.js

React and Fluent libraries are not included in the package because they are shared, therfore the size of bundle.js is significantly smaller.

Ref：<https://learn.microsoft.com/zh-cn/power-apps/developer/component-framework/react-controls-platform-libraries>
React controls & platform libraries (Preview) - Power Apps | Microsoft Learn
