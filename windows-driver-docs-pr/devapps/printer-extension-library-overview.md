---
title: 适用于 UWP 设备应用打印机扩展库概述
description: 本主题介绍了打印机扩展库，则可帮助设备制造商的库编写他们的打印机的 UWP 设备应用程序。
ms.assetid: A47B17CE-BF5A-4C02-807C-890F315A13E0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de9fbe871c89b268ce541dd03816077cb55c8f3b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323389"
---
# <a name="printer-extension-library-overview-for-uwp-device-apps"></a>适用于 UWP 设备应用打印机扩展库概述


本主题介绍了打印机扩展库，则可帮助设备制造商的库编写他们的打印机的 UWP 设备应用程序。 打印机扩展插件库是随[打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例中，以及[作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


高级别设计目标[v4 打印机驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)体系结构旨在为 Microsoft Store 应用程序用户界面提供内置支持。 若要提供访问打印机，v4 打印驱动程序公开基于 COM 的[打印机扩展插件接口](https://go.microsoft.com/fwlink/p/?LinkID=299887)。

若要从 UWP 设备应用中访问这些接口，可以使用打印机扩展库附带的 Microsoft Store 设备应用打印机示例。 打印机扩展插件库包装的 COM 接口的 COM 实现`PrinterExtensionLib`。 这样，打印机扩展和 UWP 设备应用之间共享代码。

![打印机扩展库概述](images/373030-printer-app-architecture.png)

## <a name="span-idprinterextensionlibraryspanspan-idprinterextensionlibraryspanspan-idprinterextensionlibraryspanprinterextensionlibrary"></a><span id="PrinterExtensionLibrary"></span><span id="printerextensionlibrary"></span><span id="PRINTEREXTENSIONLIBRARY"></span>PrinterExtensionLibrary


在 PrinterExtensionLibrary 项目附带打印机示例中，有两个C#文件。 这些文件的 PrinterExtensionLib 的内容进行换行。 但其他类可能要使打印机扩展和 UWP 的设备应用程序之间共享代码添加在此层。

-   **PrinterExtensionTypes.cs**指定数很有帮助的枚举、 常量和包装 COM PrinterExtensionLib Api 的接口。

-   **PrinterExtensionAdapters.cs**指定的所有 constructable 类用于包装 COM PrinterExtensionLib Api。

您可以扩展任何需要与此项目C#介绍了常见模型层代码生成打印机扩展和/或 UWP 的设备应用程序所必需的文件。 但是，我们不建议更新现有的类，因为这将使合并任何 bug 修复，可通过更新对这些示例的难度。

## <a name="span-iddeviceappforprinterslibraryspanspan-iddeviceappforprinterslibraryspanspan-iddeviceappforprinterslibraryspandeviceappforprinterslibrary"></a><span id="DeviceAppForPrintersLibrary"></span><span id="deviceappforprinterslibrary"></span><span id="DEVICEAPPFORPRINTERSLIBRARY"></span>DeviceAppForPrintersLibrary


名为 DeviceAppForPrintersLibrary，附加项目提供帮助程序类和方法C#可用于从 UWP 设备应用中访问打印机的应用。

## <a name="span-idprinterextensionhelperlibraryspanspan-idprinterextensionhelperlibraryspanspan-idprinterextensionhelperlibraryspanprinterextensionhelperlibrary"></a><span id="PrinterExtensionHelperLibrary"></span><span id="printerextensionhelperlibrary"></span><span id="PRINTEREXTENSIONHELPERLIBRARY"></span>PrinterExtensionHelperLibrary


为将C#接口、 类和方法添加到在 JavaScript 中受支持的内容，此项目将创建一个 WinMD 文件。 WinMD 文件用于指定 Windows 运行时 Api。 此外，可以使用此库公开特定于 Microsoft Store 设备应用程序，例如，分析出不同的激活上下文，或创建 toast 通知的用户界面的方便对象。

-   **PrintHelperClass.cs**包括 PrinterExtensionLibrary 命名空间，以便将它们公开给应用程序中的 JavaScript 层。 PrintTicket 和 Bidi，它还包括一些便捷方法。

-   **PrinterNotificationHelper.cs**演示如何显示 toast 通知的用户界面。

**请注意**  **输出类型**对指定程序集是 for PrinterExtensionHelperLibrary**应用程序**页的项目属性窗口。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[打印机扩展插件接口 （v4 打印驱动程序）](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[作业管理 （v4 打印机驱动程序）](https://msdn.microsoft.com/library/windows/hardware/dn265419)

[设备维护 （v4 打印机驱动程序）](https://msdn.microsoft.com/library/windows/hardware/dn265274)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用程序 （分步指南）](step-1--create-a-uwp-device-app.md)

[创建设备元数据对 UWP 设备应用 （分步指南）](step-2--create-device-metadata.md)

 

 






