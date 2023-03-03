# PACF 2. Implementing component logic & Adding style to the code component （CSS）

## ComponentFramework.StandardControl  是标准组件的接口，而Reat组件是 ComponentFramework.ReactControl

## StandardControl.init

| 参数 | 类型 | 必填 | 描述 |
| ---- | ---- | ---- | ---- |
| context | Context | 是 | 包含参数、组件元数据和接口函数的输入属性。 |
| notifyOutputChanged | function | 否 | 用于通知框架它有新输出的方法。 |
| state | Dictionary | 否 | 从上一会话中的 setControlState 保存的组件状态。 |
| container | HTMLDivElement | 否 | 要渲染的 div 元素。 |

```ts
public init(context: ComponentFramework.Context<IInputs>, notifyOutputChanged: () => void, state: ComponentFramework.Dictionary, container:HTMLDivElement)
{
    this._labelElement = document.createElement("label");
    this._labelElement.setAttribute("class", "HelloWorldColor");
    container.appendChild(this._labelElement);
}
```

* 用于初始化组件实例。 组件可以启动远程服务器调用和其他初始化操作。
* 此处无法初始化数据集值，请使用 updateView 方法来实现。
* trackContainerResize最好在组件init方法中调用一次，获取组件需要的来自容器的布局信息。

### trackContainerResize

如果组件需要根据容器大小发生变化，需要调用这个函数，这样组件就能获得 allocatedWidth 或 allocatedHeight。

When you call the trackContainerResize(true) method, the context.mode.allocatedWidth and context.mode.allocatedHeight will be provided inside the updateView method of the code component.

## StandardControl.updateView

当属性包中的任何值发生变化时，将调用此方法。 这包括字段值、数据集、全局值（例如容器高度和宽度）、离线状态、组件元数据值（例如标签、可见性等）。

```ts
public updateView(context: ComponentFramework.Context<IInputs>): void
{
    this._labelElement.innerText = "Hello World! (TS)";
}
```

## StandardControl.getOutputs

在组件的输入属性接收新数据之前由框架调用。 根据manifest中定义的命名法返回一个对象，期望属性标记为绑定的对象 [s]。

```ts
public getOutputs(): IOutputs
{
    return {
        value: this._value
    };
}
```

## StandardControl.getOutputs

当要从 DOM 树中删除组件时调用此方法。 使用它进行清理并释放组件正在使用的任何内存。

```ts
public destroy(): void
{
    this.button.removeEventListener("click", this.onButtonClick);
}
```

Ref: <https://learn.microsoft.com/zh-cn/power-apps/developer/component-framework/implementing-controls-using-typescript?tabs=before#add-properties-for-the-control>
Create your first component using Power Apps Component Framework in Microsoft Dataverse - Power Apps | Microsoft Learn

## CSS

1. 当您使用 CSS 为您的代码组件实现样式时，请确保使用自动生成的 CSS 类将 CSS 限定在您的控件范围内，该 CSS 类应用于组件的容器 DIV 元素。
2. 如果您的 CSS 是全局范围的，它可能会破坏呈现代码组件的表单或屏幕的现有样式。
3. 如果使用第三方 CSS 框架，请使用已命名空间的该框架版本，或者手动或使用 CSS 预处理器将该框架包装在命名空间中。

***
Power Apps 组件框架使用 RESX Web 资源来管理任何用户界面上显示的本地化字符串。 支持本地化的资源也注册在资源节点中。
***

### RESX Web (使用方式类似 i18n)

* 使用这些 Web 资源来管理您定义的任何用户界面中的本地化字符串或您将显示的错误消息。
* RESX 网络资源包含使用 RESX XML 格式定义的单一语言的键和本地化字符串值。 RESX 是一种用于为 Windows 应用程序定义本地化资源的通用格式，因此有可用于处理此类文件的通用工具，并且本地化供应商将熟悉如何使用它们。 当文件在 CRM 中作为 Web 资源发布时，它将被转换为 JSON 格式，在需要时将其下载到应用程序。

Ref: <https://learn.microsoft.com/zh-cn/power-apps/developer/model-driven-apps/resx-web-resources>
String (RESX) web resources (model-driven apps) - Power Apps | Microsoft Learn
