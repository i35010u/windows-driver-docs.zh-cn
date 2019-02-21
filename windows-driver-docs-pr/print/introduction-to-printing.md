---
title: 打印简介
description: 打印简介
ms.assetid: 8a2e0151-6d40-493d-9757-42350a9e6220
keywords:
- 打印 WDK
- 呈现组件 WDK 打印
- 配置组件 WDK 打印
- 组件 WDK 打印
- WDK 打印体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5f4a853dc7dbe9c28913fd6070a37c4d7c5d284
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534247"
---
# <a name="introduction-to-printing"></a>打印简介

Microsoft Windows 打印体系结构由打印后台处理程序和打印机驱动程序的一组组成。 通过调用独立于设备的函数，应用程序可以创建打印作业，并将其发送到多个设备。 这包括激光打印机矢量绘图，光栅打印机和传真计算机。

打印机驱动程序包括呈现组件和配置组件。 *呈现组件*图形命令将为打印机使用呈现页面上的图像的数据格式的应用程序。 *配置组件*包含一个用户界面组件，使用户能够控制打印机的可选择的选项和通信打印机的配置和功能的应用程序程序接口。

当 Microsoft Win32 GDI 应用程序打印时，它会调用 Win32 API 中的 GDI 函数。 这些函数将信息传递给 GDI 图形引擎。 GDI 图形引擎任一假脱机的绘制说明*增强型图元文件 (EMF)* 文件或打印机驱动程序，以及呈现可以发送到后台处理程序的可打印图像。 后台处理程序组件解释 EMF 文件和它们可以插入到数据流中的页面布局信息和作业控制指令。 数据流至串行、 并行或与目标打印机的 I/O 端口相关联的网络端口驱动程序，然后将发送后台处理程序。 此外，如果打印到 XPS 设备，通过 GDI 到 XPS 转换组件转换 GDI 打印命令并将其 XPS 打印路径发送打印作业。

XPS 打印路径，在打印机驱动程序基于 XML 纸张规范 (XPS) 上。 当一个应用程序，Microsoft Win32 XPS 打印时，应用程序中的 XPS 打印 API 调用 XPS 函数。 当将它打印到的队列[XPSDrv 的打印机驱动程序](xpsdrv-printer-drivers.md)，后台处理程序将 XPS 假脱机文件传递给呈现和输出设备直接。 到 GDI 设备打印 XPS 文件时，它被转换为通过 GDI 转换模块到 XPS EMF 文件。 它然后通过 GDI 打印路径的方式类似于 Win32 GDI 应用程序中发送。

Windows Presentation Foundation (WPF) 应用程序在 XPS 后台打印文件格式中调用到后台处理到后台处理程序的 XPS 文档的 WPF 打印支持函数。 如时从 Win32 XPS 的应用程序，打印后台处理程序将打印到打印队列与 XPSDrv 打印机驱动程序时，后台处理程序会将其原始格式的假脱机的文件传递给呈现和输出到打印机的 XPSDrv 打印机驱动程序。 当具有基于 GDI 的打印机打印后台处理程序时，版本 3 的打印机驱动程序，后台处理程序将数据发送 XPS 后台打印文件格式转换为的 EMF 文件的 GDI 转换模块。 然后将数据发送到打印基于 GDI 的打印机驱动程序。 有关这些数据路径的详细信息，请参阅[Windows 打印路径概述](windows-print-path-overview.md)。 有关 XPS 的详细信息，请参阅[XML 纸张规范概述](https://msdn.microsoft.com/library/windows/hardware/dn641615)。

后台处理程序和驱动程序组件是可替换，因此硬件供应商可以轻松地添加对新硬件的支持。 有关打印后台处理程序和驱动程序组件的详细信息，请参阅以下各节：

[打印后台处理程序体系结构](print-spooler-architecture.md)

[打印机驱动程序体系结构](printer-driver-architecture.md)

支持新的打印机通常需要只使用其中一个 Microsoft 提供的打印机驱动程序中创建新的数据文件使用。 有关 Microsoft 打印机驱动程序的详细信息，请参阅[打印机驱动程序概述](printer-driver-overview.md)。

可以自定义 Microsoft 通用打印机驱动程序和 Microsoft Postscript 打印机驱动程序的行为。 有关详细信息，请参阅[自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)。 此外可以自定义打印后台处理程序。 有关详细信息，请参阅[自定义打印后台处理程序组件](print-spooler-components.md)。

其他部分介绍了以下主题：

[终端服务器打印](terminal-server-printing.md)

[USB 打印](usb-printing.md)

[蓝牙打印](bluetooth-printing.md)

[打印机驱动程序测试和调试](printer-driver-testing-and-debugging.md)
