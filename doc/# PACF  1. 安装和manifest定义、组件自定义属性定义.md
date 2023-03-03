# PACF  1. 安装和manifest定义、组件自定义属性定义

## require install

1. Visual Studio Code (VSCode) (Ensure the Add to PATH option is select)
2. node.js (LTS version is recommended)
3. Microsoft Power Platform CLI (Use either Power Platform Tools for Visual Studio Code or Power Platform CLI for Windows)
4. .NET Build tools by installing following: (At minimum select the workload .NET build tools.)
    1. Visual Studio 2022 Visual Studio 2022 for Windows & Mac. Build Tools for Visual Studio 2022

## CLI 预创建

pac pcf init --namespace SampleNamespace --name LinearInputControl --template field --run-npm-install

* pac：Power Apps CLI命令行工具的名称
* pcf：PowerApps组件框架（PCF）的缩写
* init：用于初始化新的PCF控件项目的命令
* --namespace SampleNamespace：用于指定控件的命名空间。命名空间应该是唯一的，以避免与其他控件产生冲突。
* --name LinearInputControl：用于指定控件的名称。控件的名称也应该是唯一的。(所以你应该在LinearInputControl文件夹中进行开发)
* --template field：用于指定控件模板的类型。field模板用于创建一个新的自定义字段控件。
* --run-npm-install：如果设置了此参数，则在创建新的PCF控件项目后自动运行npm install命令，以安装所有依赖项。

## ControlManifest.Input.xml

### <manifest> & <control>

```xml
  <control namespace="SampleNamespace" constructor="LinearInputControl" version="0.0.1" display-name-key="LinearInputControl" description-key="LinearInputControl description" control-type="standard" >

```

Name Description Type Required Available for
namespace 定义组件的命名空间 or （Defines the object prototype of the component） 仅限字母或数字 是 模型驱动和画布应用
constructor 用于初始化组件的方法 仅限字母或数字 是 模型驱动和画布应用
control-type 控件是标准控件还是React控件。virtual的值表示使用平台React库的React控件。虚拟控件是公开预览功能。详细信息：React controls & platform libraries (Preview) standard|virtual 否 模型驱动和画布应用
description-key 定义将在UI上看到的组件描述 字符串 否 模型驱动和画布应用
display-name-key 定义在UI上显示的控件名称 字符串 是 模型驱动和画布应用
preview-image 将用于自定义屏幕上显示组件预览的图像 字符串 否 仅限模型驱动应用
version 定义符合语义化版本规范的组件版本 字符串 是 模型驱动和画布应用

### <type-group name="numbers"> <type>

```xml
 <type-group name="numbers">
      <type>Whole.None</type>
      <type>Currency</type>
      <type>FP</type>
      <type>Decimal</type>
   </type-group>
```

定义一组控件的类型信息

The resolvable type groupings are as follows:

* Strings: SingleLine.Text, Multiple, SingleLine.TextArea, SingleLine.Email, SingleLine.Phone, SingleLine.URL, SingleLine.Ticker.
* Numbers: Decimal, FP, Whole.None, Currency.
* Dates: DateAndTime.DateAndTime, DateAndTime.DateOnly.

Type 文档记录了 Enum type 的例子，但是使用的标签是<property> ？？？

### <property>

```xml
   <property name="sampleProperty"
      display-name-key="Property_Display_Key"
      description-key="Property_Desc_Key"
      of-type="SingleLine.Text"
      usage="bound"
      required="true" />

```

属性节点定义组件期望从 Microsoft Dataverse 获得的特定的、可配置的数据。(就和画布应用创建组件一样)

Attribute Description
name 属性名称
display-name-key 在用户界面上显示的属性名称
description-key 在用户界面上显示的属性描述
of-type-group 当您想引用特定类型组的名称时，请使用of-type-group属性。在此示例中，我们引用了先前创建的名称为“numbers”的类型组。
usage 具有两个属性，即绑定和输入。

### <resources> & <code> & <css> & <img> & <resx> & <platform-library>

```xml
<resources>
   <code path="index.ts"
   order="1" />
   <css path="css/LinearInputControl.css"
   order="1" />
</resources>
```

Manifest.Input.xml 中的resources是指组件实现其可视化所需的资源文件

<code> & <css> & <img> & <resx>

* path 资源地址（本地）
* order load顺序

<platform-library> This element is used in the React controls & platform libraries (Preview) .

## 通过 Manifest 生成 d.ts

```CLI
npm run refreshTypes
```
