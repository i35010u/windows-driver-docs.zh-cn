---
title: 打印简介
description: 打印简介
ms.assetid: 8a2e0151-6d40-493d-9757-42350a9e6220
keywords:
- 打印 WDK
- 呈现组件 WDK 打印
- 配置组件 WDK 打印
- 组件 WDK 打印
- 体系结构 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9b74729c87939b65efca7bac588cb390899c992
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205883"
---
# <a name="introduction-to-printing"></a>打印简介

Microsoft Windows 打印体系结构包含打印后台处理程序和一组打印机驱动程序。 通过调用与设备无关的函数，应用程序可以创建打印作业并将其发送到多个设备。 这包括激光打印机、矢量绘图仪、光栅打印机和传真计算机。

打印机驱动程序包括呈现组件和配置组件。 *呈现组件*将图形命令从应用程序转换为打印机用于在页面上呈现图像的数据格式。 *配置组件*包含用户界面组件，用户可以使用该组件来控制打印机的可选择选项以及将打印机的配置和功能与应用程序通信的程序接口。

当 Microsoft Win32 GDI 应用程序打印时，它将调用 Win32 API 中的 GDI 函数。 这些函数将信息传递给 GDI 图形引擎。 GDI 图形引擎可以将绘图指令线轴作为 *增强型图元文件 (EMF) * 文件，或者连同打印机驱动程序一起呈现可发送到后台处理程序的可打印图像。 后台处理程序组件解释 EMF 文件，它们可以将页面布局信息和作业控制指令插入到数据流中。 然后，后台处理程序将数据流发送到与目标打印机的 i/o 端口关联的串行、并行或网络端口驱动程序。 此外，如果打印到 XPS 设备，GDI 打印命令将通过 "GDI 转换为 XPS" 组件转换，打印作业将按 XPS 打印路径向下发送。

在 XPS 打印路径中，打印机驱动程序基于 XML 纸张规范 (XPS) 。 当 Microsoft Win32 XPS 应用程序打印时，应用程序将调用 XPS 打印 API 中的 XPS 函数。 当它打印到带有 [XPSDrv 打印机驱动程序](xpsdrv-printer-drivers.md)的队列时，后台处理程序将 XPS 假脱机文件直接传递到设备以进行呈现和输出。 将 XPS 文件打印到 GDI 设备后，它将通过 XPS 到 GDI 转换模块转换为 EMF 文件。 然后，它通过 GDI 打印路径发送，其方式与 Win32 GDI 应用程序类似。

Windows Presentation Foundation (WPF) 应用程序调用 WPF 打印支持功能将 XPS 文档以 XPS 假脱机文件格式后台处理到后台处理程序。 与从 Win32 XPS 应用程序进行打印时一样，当后台处理程序通过 XPSDrv 打印机驱动程序打印到打印队列时，后台处理程序将原始格式的假脱机文件传递给 XPSDrv 打印机驱动程序，以便在打印机上呈现和输出。 当后台处理程序打印到具有基于 GDI 的版本3打印机驱动程序的打印机时，后台处理程序会将 XPS 假脱机文件格式的数据发送到 GDI 转换模块，以便转换到 EMF 文件。 然后，它会将数据发送到基于 GDI 的打印机驱动程序以进行打印。 有关这些数据路径的详细信息，请参阅 [Windows 打印路径概述](windows-print-path-overview.md)。 有关 XPS 的详细信息，请参阅 [XML 纸张规范概述](/previous-versions/windows/hardware/design/dn641615(v=vs.85))。

后台处理程序和驱动程序组件是可替换的，因此硬件供应商可以轻松地添加对新硬件的支持。 有关打印后台处理程序和驱动程序组件的详细信息，请参阅以下部分：

[打印后台处理程序体系结构](print-spooler-architecture.md)

[打印机驱动程序体系结构](printer-driver-architecture.md)

支持新的打印机通常只需要创建新的数据文件，以便与 Microsoft 提供的打印机驱动程序之一一起使用。 有关 Microsoft 打印机驱动程序的详细信息，请参阅 [打印机驱动程序概述](printer-driver-overview.md)。

你可以自定义 Microsoft 通用打印机驱动程序和 Microsoft Postscript 打印机驱动程序的行为。 有关详细信息，请参阅 [自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)。 你还可以自定义打印后台处理程序。 有关详细信息，请参阅 [自定义打印后台处理程序组件](print-spooler-components.md)。

其他部分涵盖以下主题：

[终端服务器打印](terminal-server-printing.md)

[USB 打印](usb-printing.md)

[蓝牙打印](bluetooth-printing.md)

[打印机驱动程序测试和调试](printer-driver-testing-and-debugging.md)