---
title: V4 驱动程序 UI 体系结构
description: V4 驱动程序体系结构的高级设计目标是为 Microsoft Store 应用用户界面提供内置支持。
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 90c1d2299dc5a3bfd8a418dc8c5b5cb7916fbde6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785907"
---
# <a name="v4-driver-ui-architecture"></a>V4 驱动程序 UI 体系结构

V4 驱动程序体系结构的高级设计目标是为 Microsoft Store 应用用户界面提供内置支持。

使用的基于应用程序的 UI 范例是此示例的一个清晰示例。 UWP 设备应用为用户提供了 Microsoft Store 应用 UI 中支持的全屏体验。 UWP 设备应用进行打印为打印首选项提供可扩展性，并为支持 v4 打印驱动程序的打印机提供打印机通知。 UWP 设备应用进行打印还在新的 "开始" 屏幕上提供打印设备的可见性。

当用户在 Windows 桌面上运行现有应用程序时，打印机扩展应用程序支持打印首选项和打印机通知。 虽然这些应用程序的 Ui 差别很大，但每个 ui 针对鼠标和键盘用户进行了优化，但不管 UI 如何，业务逻辑和 v4 打印驱动程序的连接仍然可以类似。

下图显示了在 GitHub 上提供的 [V4 打印驱动程序和打印机扩展示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples) 的 Microsoft Store 设备应用程序的高级体系结构。

![自定义 ui 体系结构概述](images/v4custuiarch.png)

如前面的关系图中所示，基于模型/视图/控制器的体系结构使应用可以在以 c # 编写的模型层上共享代码。

## <a name="extending-printerextensionlibrary"></a>扩展 PrinterExtensionLibrary

可以使用新的类或通过扩展提供的类集来扩展各个示例中随附的 PrinterExtensionLibrary 项目。 由于 Microsoft 定期对示例代码进行更新，因此，我们建议合作伙伴应最大程度地减少对提供的源文件所做的代码更改的数量。 对于正在扩展提供的类集的合作伙伴，我们建议您将现有类标记为 "partial"，并在单独的源文件中添加新的函数或重写。

## <a name="sharing-compiled-binaries-between-uwp-apps-and-desktop-apps"></a>在 UWP 应用和桌面应用之间共享已编译的二进制文件

Microsoft Store 设备应用和打印机扩展示例附带的 PrinterExtensionLibrary 项目使用相同的源代码，但生成代码，使其可在项目之间移植，而无需为每个项目单独生成。 若要使 PrinterExtensionLibrary 项目的代码可移植，你必须将该项目转换为可移植类库。 执行以下步骤以进行转换。

1. 在 Microsoft Visual Studio 中，单击 "**文件**  >  " "**新建**  >  **项目**"，然后在 "**搜索已安装的模板**" 框中搜索 "可移植的"。

2. 选择 "可移植类库" "Visual c #"，然后在 " **名称** " 文本框中提供项目的名称，然后单击 **"确定"。**

3. 将现有 PrinterExtensionLibrary 项目中的源代码复制到新项目中。

4. 右键单击可移植类库项目，然后选择 " **卸载**"。 然后打开 .csproj 文件，并将以下部分添加到文件中，就在文档中的最后一个标记之前。

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

5. 如果由于 COM 引用而看到警告，请将以下内容添加到 \<PropertyGroup\> 标记：

```xml
<ResolveComReferenceSilent>true</ResolveComReferenceSilent>
```

## <a name="api-for-print-ui-scenarios"></a>用于打印 UI 方案的 API

已将 API 作为 v4 打印驱动程序模型的一部分进行开发，以支持打印机扩展和 UWP 设备应用进行打印。 在高级别中，打印首选项方案使用 PrintTicket、PrintCapabilities 和新的属性包获取并存储其所有信息。 打印机通知由基于双向通信)  (双向通信的新事件系统驱动，这一新的系统使用客户端和服务器之间的 AsyncUI 协议。 此 API 以数据为中心的性质意味着一个应用程序可以轻松地支持多个设备。

需要以这样一种方式生成打印机扩展：如果请求的数据不可用，则可以适当地降低这些扩展。 例如，如果特定的 PrintCapabilities 功能不可用，或者某个属性包中的属性不可用，则不会阻止其余应用程序正常运行。 当访问属性包或属性包中的特定属性时，应用程序应使用 try-catch 语法，以确保引发的任何异常不会导致应用程序崩溃。 有关详细信息，请参阅 [打印机扩展接口](/windows-hardware/drivers/ddi/printerextension/index#interfaces)。

## <a name="related-resources"></a>相关资源

[打印机扩展接口](/windows-hardware/drivers/ddi/printerextension/#interfaces)

[GitHub 上的 v4 打印驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/print/v4PrintDriverSamples)
