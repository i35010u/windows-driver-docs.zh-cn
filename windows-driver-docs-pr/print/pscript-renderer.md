---
title: Pscript 渲染器
description: Pscript 渲染器
keywords:
- PostScript 打印机驱动程序 WDK 打印，呈现器
- Pscript WDK 打印，呈现器
- 呈现器 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c57617def607b0b38a91ced7b5514b7667853232
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807147"
---
# <a name="pscript-renderer"></a>Pscript 渲染器





Pscript 呈现器作为 [打印机图形 DLL](printer-graphics-dll.md) 实现，因此，导出由 Microsoft 设备驱动程序接口定义的函数， (DDI) 用于图形驱动程序。 当应用程序调用图形设备接口 (GDI) 函数将文本和图像发送到打印机设备时，内核模式图形引擎将调用呈现器的图形 DDI 函数。 这些图形 DDI 函数有助于在绘图打印作业的页面图像时使用 GDI。

呈现器还负责将呈现的图像数据以及打印机命令序列发送到打印后台处理程序，然后将数据流和命令定向到打印机硬件。

你可以通过提供 [呈现插件](rendering-plug-ins.md)来修改 Pscript 的呈现操作，该插件在标题为 " [自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)" 部分中进行了介绍。

 

 




