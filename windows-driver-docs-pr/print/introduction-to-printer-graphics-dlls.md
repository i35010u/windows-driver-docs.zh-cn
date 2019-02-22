---
title: 打印机图形 Dll 简介
description: 打印机图形 Dll 简介
ms.assetid: 3f7ce476-6bef-4a80-ae2a-2a63e891dda1
keywords:
- 打印机图形 DLL WDK 有关打印机图形 DLL
- 图形 DLL WDK 打印机，有关打印机图形 DLL
- 图形 DLL WDK 打印机
- 打印机图形 DLL WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 846d52929fa96f14d74b882d816c454a97f4fef7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547826"
---
# <a name="introduction-to-printer-graphics-dlls"></a>打印机图形 Dll 简介


打印机图形 Dll 实现 Drv 前缀图形中所述的 DDI 函数[使用图形 DDI](https://msdn.microsoft.com/library/windows/hardware/ff570139)。 这些 Dll 具有以下两个职责：

-   帮助 GDI 呈现打印作业。

    打印机图形 DLL 可以提供图形 DDI 绘图函数来处理必须以特定于设备的方式执行，因此无法以独占方式通过 GDI 的呈现引擎处理的绘制操作。

-   将呈现的数据流传递到后台处理程序。

    打印机图形 Dll 通常生成原始数据类型中的输出流。

打印机图形 DLL 必须提供的呈现帮助量为打印机的特定于类型，具体取决于硬件的绘图功能，并包括以下方案：

-   GDI 呈现引擎将执行所有呈现，使用 GDI 管理面。 图形 DLL 不提供任何 DDI 绘图函数。

-   图形 DLL 提供了一些图形 DDI 绘图函数与 GDI 的呈现引擎，可结合使用 GDI 管理面。 图形 DDI 的绘图功能提供的图形 DLL 可以选择调用返回到 GDI 呈现引擎[GDI 支持服务](https://msdn.microsoft.com/library/windows/hardware/ff566714)。

-   图形 DLL 通过提供图形 DDI 来做到所有呈现绘图功能和使用设备管理面。

例如， [Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)(Unidrv) 使用 GDI 管理面，并提供一些图形 DDI 的绘图功能，而[Microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md)使用设备管理面。

有关提供图形驱动程序的呈现帮助的详细信息，请参阅[图面类型](https://msdn.microsoft.com/library/windows/hardware/ff569900)并[使用图形 DDI](https://msdn.microsoft.com/library/windows/hardware/ff570139)。

以下两个图形说明了应用程序可创建使用 GDI 的打印作业时，会发生的数据流。 在这些数字组合 EMF 录制和播放。

第一个关系图描绘了用户模式打印机图形 DLL。

**请注意**  只能在用户模式下执行 Windows Vista 中打印机图形 Dll。 有关详细信息，请参阅[选择用户模式或内核模式](choosing-user-mode-or-kernel-mode.md)。

 

![说明用户模式打印机图形 dll 的关系图](images/usrmdprt.png)

第二个关系图描绘了内核模式打印机图形 DLL。

![打印作业使用的数据流，内核模式打印机图形 dll](images/gdiprint.png)

请注意，在这些关系图的如果从 GDI 的输出格式*增强型图元文件 (EMF)*，打印机图形 DLL 不会收到该作业，直到 EMF 打印处理器播放 EMF 记录。 另请注意 EMF 打印处理器，对非 EMF 更改输出格式。

图说明了完全本地环境。 如果打印机连接到服务器，EMF 记录通常由 GDI 呈现引擎 (GRE) 的客户端的副本，然后后台处理到发送到服务器的本地文件。 后台处理程序的服务器的副本读取的文件并将记录发送到服务器的 EMF 打印处理器和 GRE 的服务器的副本调用服务器的打印机图形 DLL。

 

 




