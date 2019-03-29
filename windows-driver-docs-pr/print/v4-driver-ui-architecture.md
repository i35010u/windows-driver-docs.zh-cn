---
title: V4 驱动程序 UI 体系结构
description: V4 驱动程序体系结构的高级别设计目标是为 Microsoft Store 应用程序用户界面提供内置支持。
ms.assetid: 6318E480-C567-4866-8E88-B19904408C59
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: ddb6a7e4feb816b79aa9f366bff0883f79b7c120
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575454"
---
# <a name="v4-driver-ui-architecture"></a>V4 驱动程序 UI 体系结构

V4 驱动程序体系结构的高级别设计目标是为 Microsoft Store 应用程序用户界面提供内置支持。

基于应用程序的 UI 范例，它将使用的是一个清晰的示例。 UWP 的设备应用程序为用户提供支持的 Microsoft Store 应用 UI 中的全屏体验。 UWP 打印设备应用程序提供有关打印首选项，可扩展性和打印机通知的打印机支持 v4 打印驱动程序。 UWP 设备应用程序的打印也提供新的开始屏幕上打印设备的可见性。

当用户在 Windows 桌面上运行现有应用程序时，打印机扩展应用程序支持打印首选项和打印机通知。 虽然这些应用程序的 Ui 是大不相同，其中一个定制的触摸和其他优化鼠标和键盘用户，业务逻辑和 v4 打印驱动程序的连接仍然可以类似，而不考虑用户界面。

下图显示了适用于的 Microsoft Store 设备应用的高级别体系结构[v4 打印机驱动程序和打印机扩展插件示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples)GitHub 上提供。

![自定义 ui 体系结构概述](images/v4custuiarch.png)

上图中所示，/视图/控制器基于模型的体系结构能使应用程序共享模型层，以编写代码C#。

## <a name="extending-printerextensionlibrary"></a>扩展 PrinterExtensionLibrary

可以扩展使用新的类，或通过扩展提供设置的类中的各种示例随附的 PrinterExtensionLibrary 项目。 由于 Microsoft 定期对示例代码进行更新，因此建议合作伙伴应尽量减少它们对提供的源文件进行代码更改的数量。 对于要扩展的类提供的组的合作伙伴，我们建议您将标记为"部分"的现有类，并在单独的源代码文件中添加新的函数或重写。

## <a name="sharing-compiled-binaries-between-uwp-apps-and-desktop-apps"></a>共享编译 UWP 应用和桌面应用程序之间的二进制文件

在 Microsoft Store 设备应用程序和打印机扩展插件示例中提供的 PrinterExtensionLibrary 项目利用相同的源代码，但它可能会很有价值，以生成的代码，因此无需为每个单独构建项目之间可移植项目。 若要提高 PrinterExtensionLibrary 项目的代码可移植性，必须将项目转换为可移植类库。 执行以下步骤以进行转换。

1. 在 Microsoft Visual Studio 中，单击**文件** &gt; **新建** &gt; **项目**，然后在搜索"可移植"**搜索已安装的模板**框。

2. 选择可移植类库 Visual C#，然后提供在项目的名称**名称**文本框中，然后单击**确定。**

3. 将源代码从现有 PrinterExtensionLibrary 项目复制到新的项目。

4. 右键单击你的可移植类库项目并选择**Unload**。 然后打开.csproj 文件并将以下节添加到你的文件，只需在文档中的最后一个标记之前。

```xml
  <ItemGroup>
    <COMReference Include="PrinterExtensionLib">
      <Guid>{91CE54EE-C67C-4B46-A4FF-99416F27A8BF}</Guid>
      <VersionMajor>1</VersionMajor>
      <VersionMinor>0</VersionMinor>
      <Lcid>0</Lcid>
      <WrapperTool>tlbimp</WrapperTool>
      <Isolated>False</Isolated>
      <EmbedInteropTypes>True</EmbedInteropTypes>
    </COMReference>
  </ItemGroup>
```

5. 如果您看到由于 COM 引用的警告，添加以下&lt;PropertyGroup&gt;标记：

```xml
<ResolveComReferenceSilent>true</ResolveComReferenceSilent>
```

## <a name="api-for-print-ui-scenarios"></a>打印 UI 方案的 API

V4 打印驱动程序模型以支持打印的打印机扩展和 UWP 的设备应用程序的一部分开发了一个 API。 在高级别中，打印首选项方案使用 PrintTicket 和 PrintCapabilities 新的属性包来获取并存储其所有的信息。 此新系统将使用客户端和服务器之间的 AsyncUI 协议和打印机通知驱动的双向通信 (Bidi) 架构中，为基础的新事件处理系统。 此 API 的以数据为中心性质意味着一个应用程序可以轻松地支持多个设备。

打印机扩展插件需要生成的方式，它们可以妥善降级如果所请求的数据不可用。 例如，如果特定的 PrintCapabilities 功能将不可用，或者其中一个属性包中的属性将不可用，则这应阻止其余应用程序正常运行。 在访问属性包或在属性包中的特定属性时，应用应使用 try catch 语法为了确保引发的任何异常不会导致应用崩溃。 有关详细信息，请参阅[打印机扩展插件接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/index#interfaces)。

## <a name="related-resources"></a>相关资源

[打印机扩展插件接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/#interfaces)

[GitHub 上的 v4 打印驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples)



