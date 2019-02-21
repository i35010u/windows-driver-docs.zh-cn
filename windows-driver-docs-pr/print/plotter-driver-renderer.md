---
title: 绘图器驱动程序呈现器
description: 绘图器驱动程序呈现器
ms.assetid: 54aac978-6344-41b3-97ea-e78816fb94dc
keywords:
- 绘图器驱动程序 WDK 打印，呈现器
- MSPlot WDK 打印，呈现器
- 呈现器 WDK MSPlot
- 图形 DDI 函数 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53553fab1f200eaab54c48e03da6c2b26e1cf324
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541889"
---
# <a name="plotter-driver-renderer"></a>绘图器驱动程序呈现器





绘图器驱动程序呈现器作为[打印机图形 DLL](printer-graphics-dll.md) ，并因此将导出定义由 Microsoft 设备驱动程序接口 (DDI) 的图形驱动程序的函数。 当应用程序调用图形设备接口 (GDI) 函数将映像发送到绘图仪时，内核模式图形引擎会调用呈现器的图形 DDI 函数。 这些图形 DDI 函数帮助 GDI 绘制打印作业的页面图像。

程序还负责发送呈现器呈现图像数据，以及绘图器命令序列，打印后台处理程序，后者随后将定向映像和命令指向绘图器硬件。

 

 




