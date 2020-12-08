---
title: 绘图仪驱动程序渲染器
description: 绘图仪驱动程序渲染器
keywords:
- 绘图仪驱动程序 WDK 打印，呈现器
- MSPlot WDK 打印，呈现器
- 呈现器 WDK MSPlot
- 图形 DDI 函数 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2956604ffa980ffc1d0cf67d4d2cc03ecf94fe93
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807593"
---
# <a name="plotter-driver-renderer"></a>绘图仪驱动程序渲染器





绘图仪驱动程序呈现器以 [打印机图形 DLL](printer-graphics-dll.md) 的形式实现，因此，导出由 Microsoft 设备驱动程序接口定义的函数 (用于图形驱动程序的 DDI) 。 当应用程序调用图形设备接口 (GDI) 函数将图像发送到绘图仪时，内核模式图形引擎将调用呈现器的图形 DDI 函数。 这些图形 DDI 函数有助于在绘图打印作业的页面图像时使用 GDI。

呈现器还负责将呈现的图像数据以及绘图仪命令序列发送到打印后台处理程序，然后将映像和命令定向到绘图仪硬件。

 

 




