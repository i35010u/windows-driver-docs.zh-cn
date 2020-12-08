---
title: 打印机图形 DLL 简介
description: 打印机图形 DLL 简介
keywords:
- 打印机图形 DLL WDK，关于打印机图形 DLL
- 图形 DLL WDK 打印机，关于打印机图形 DLL
- 图形 DLL WDK 打印机
- 打印机图形 DLL WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd827b6fb3af3fbc6dbdfaf479f4ae42bcd5b49
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796679"
---
# <a name="introduction-to-printer-graphics-dlls"></a>打印机图形 DLL 简介


打印机图形 Dll 实现 [使用图形 ddi](../display/using-the-graphics-ddi.md)中所述的 winspool.drv 前缀图形 DDI 函数。 这些 Dll 具有以下两项职责：

-   帮助在呈现打印作业时使用 GDI。

    打印机图形 DLL 可以提供图形 DDI 绘图函数来处理必须以特定于设备的方式执行的绘图操作，因此不能以独占方式处理 GDI 的呈现引擎。

-   将呈现的数据流传递到后台处理程序。

    打印机图形 Dll 通常在 [原始数据类型](raw-data-type.md) 中生成输出流 (包括命令序列) 后台处理程序可以通过 *打印监视器* 发送到打印机硬件。

打印机图形 DLL 必须提供的呈现帮助数取决于特定于硬件的绘图功能，并包括以下方案：

-   GDI 呈现引擎使用 GDI 管理的图面完成所有呈现。 图形 DLL 不提供任何 DDI 绘图函数。

-   图形 DLL 提供了一些图形 DDI 绘图函数，可使用 GDI 管理的图面与 GDI 的渲染引擎一起工作。 图形 DLL 提供的图形 DDI 绘图函数可以选择性地回拨到 GDI 呈现引擎的 [gdi 支持服务](../display/gdi-support-services.md)。

-   图形 DLL 通过提供图形 DDI 绘图函数并使用设备管理的图面来完成所有呈现。

例如， [Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md) (Unidrv) 使用 GDI 管理的图面并提供一些图形 DDI 绘图功能，而 [Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md) 则使用设备管理的图面。

有关在图形驱动程序中提供呈现帮助的详细信息，请参阅 [表面类型](../display/surface-types.md) 和 [使用图形 DDI](../display/using-the-graphics-ddi.md)。

下面两个图说明了应用程序使用 GDI 创建打印作业时所发生的数据流。 在这些图中组合了 EMF 记录和播放。

第一个关系图描述了用户模式打印机图形 DLL。

**注意**   在 Windows Vista 打印机中，Dll 只能在用户模式下执行。 有关详细信息，请参阅 [选择用户模式或内核模式](choosing-user-mode-or-kernel-mode.md)。

 

![说明用户模式打印机图形 dll 的关系图](images/usrmdprt.png)

第二个关系图描述了内核模式打印机图形 DLL。

![使用内核模式打印机图形 dll 打印作业数据流](images/gdiprint.png)

请注意，在这些关系图中，如果 GDI 的输出格式是 *(EMF) 的增强型图元文件*，则在 emf 打印处理器播放 emf 记录之前，打印机图形 DLL 不会接收作业。 另请注意，EMF 打印处理器将输出格式更改为非 EMF。

这些关系图演示了一个完全本地的环境。 如果打印机已连接到服务器，EMF 记录通常由 GDI 呈现引擎的客户端副本生成 (GRE) ，然后后台处理到发送到服务器的本地文件。 服务器的后台处理程序副本将读取该文件并将记录发送到服务器的 EMF 打印处理器，并使服务器的 GRE 副本调用服务器的打印机图形 DLL。

 

