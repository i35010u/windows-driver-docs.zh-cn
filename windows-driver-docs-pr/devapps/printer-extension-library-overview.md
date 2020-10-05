---
title: UWP 设备应用的打印机扩展库概述
description: 本主题介绍了打印机扩展库，这是一个可帮助设备制造商为其打印机写入 UWP 设备应用程序的库。
ms.assetid: A47B17CE-BF5A-4C02-807C-890F315A13E0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d304e031c9c06fb28c0211cf93545145e8ca040
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734201"
---
# <a name="printer-extension-library-overview-for-uwp-device-apps"></a>UWP 设备应用的打印机扩展库概述


本主题介绍了打印机扩展库，这是一个可帮助设备制造商为其打印机写入 UWP 设备应用程序的库。 打印机扩展库随 " [打印设置" 和 "打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例一起提供，还包括 [作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829) 示例。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>叙述


[V4 打印机驱动程序](../print/v4-printer-driver.md)体系结构的高级设计目标是为 Microsoft Store 应用用户界面提供内置支持。 为了提供对打印机的访问，v4 打印驱动程序会公开基于 COM 的 [打印机扩展接口](/windows-hardware/drivers/ddi/_print/)。

若要从 UWP 设备应用访问这些接口，可以使用 Microsoft Store 设备应用打印机示例附带的打印机扩展库。 打印机扩展库包装 COM 接口的 COM 实现 `PrinterExtensionLib` 。 这使得可以在打印机扩展和 UWP 设备应用之间共享代码。

![打印机扩展库概述](images/373030-printer-app-architecture.png)

## <a name="span-idprinterextensionlibraryspanspan-idprinterextensionlibraryspanspan-idprinterextensionlibraryspanprinterextensionlibrary"></a><span id="PrinterExtensionLibrary"></span><span id="printerextensionlibrary"></span><span id="PRINTEREXTENSIONLIBRARY"></span>PrinterExtensionLibrary


在打印机示例附带的 PrinterExtensionLibrary 项目中，有两个 c # 文件。 这些文件将包装 PrinterExtensionLib 的内容。 但在此层可以添加其他类，以便在打印机扩展和 UWP 设备应用之间共享代码。

-   **PrinterExtensionTypes.cs** 指定了大量有用的枚举、常量和用于包装 COM PrinterExtensionLib api 的接口。

-   **PrinterExtensionAdapters.cs** 指定用于包装 COM PrinterExtensionLib api 的所有 constructable 类。

您可以用任何必要的 c # 文件来补充此项目，这些文件描述构建打印机扩展和/或 UWP 设备应用程序所需的常见模型层代码。 但是，我们不建议更新现有的类，因为这样做会使引入通过对示例的更新提供的 bug 修复变得更加困难。

## <a name="span-iddeviceappforprinterslibraryspanspan-iddeviceappforprinterslibraryspanspan-iddeviceappforprinterslibraryspandeviceappforprinterslibrary"></a><span id="DeviceAppForPrintersLibrary"></span><span id="deviceappforprinterslibrary"></span><span id="DEVICEAPPFORPRINTERSLIBRARY"></span>DeviceAppForPrintersLibrary


其他名为 DeviceAppForPrintersLibrary 的项目提供了可用于从 UWP 设备应用访问打印机的 c # 应用程序的帮助程序类和方法。

## <a name="span-idprinterextensionhelperlibraryspanspan-idprinterextensionhelperlibraryspanspan-idprinterextensionhelperlibraryspanprinterextensionhelperlibrary"></a><span id="PrinterExtensionHelperLibrary"></span><span id="printerextensionhelperlibrary"></span><span id="PRINTEREXTENSIONHELPERLIBRARY"></span>PrinterExtensionHelperLibrary


为了将 c # 接口、类和方法转换为 JavaScript 中支持的某个内容，此项目将创建 WinMD 文件。 WinMD 文件指定 Windows 运行时 Api。 此外，此库还可用于公开特定于 Microsoft Store 设备应用的便利对象，例如分析不同激活上下文或为通知创建 toast UI。

-   **PrintHelperClass.cs** 包含 PrinterExtensionLibrary 命名空间，以便在应用程序中向 JavaScript 层公开这些命名空间。 它还包括一些用于 PrintTicket 和双向的便利方法。

-   **PrinterNotificationHelper.cs** 演示如何显示通知的 toast UI。

**注意**   PrinterExtensionHelperLibrary 程序集的**输出类型**是在 "项目属性" 窗口的 "**应用程序**" 页上指定的。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 v4 打印驱动程序](../print/v4-printer-driver.md)

[ (v4 打印驱动程序的打印机扩展接口) ](/windows-hardware/drivers/ddi/_print/)

[作业管理 (v4 打印机驱动程序) ](../print/job-management.md)

[设备维护 (v4 打印机驱动程序) ](../print/device-maintenance.md)

[双向通信](../print/bidirectional-communication.md)

[UWP 应用入门](getting-started.md)

[ (分步指南创建 UWP 设备应用) ](step-1--create-a-uwp-device-app.md)

[ (分步指南创建 UWP 设备应用的设备元数据) ](step-2--create-device-metadata.md)

