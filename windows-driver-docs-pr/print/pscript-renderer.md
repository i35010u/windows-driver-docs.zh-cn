---
title: Pscript 渲染器
description: Pscript 渲染器
ms.assetid: b1707a83-c5c9-4578-8603-7c19de4960ed
keywords:
- PostScript 打印机驱动程序 WDK 打印，呈现器
- Pscript WDK 打印，呈现器
- 呈现器 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee28253b9faab9a5bd14abaaacaa30a42b5c3fbc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357647"
---
# <a name="pscript-renderer"></a>Pscript 渲染器





作为实现 Pscript 呈现器[打印机图形 DLL](printer-graphics-dll.md) ，并因此将导出定义由 Microsoft 设备驱动程序接口 (DDI) 的图形驱动程序的函数。 当应用程序调用图形设备接口 (GDI) 函数将文本和图像发送到打印机设备时，内核模式图形引擎会调用呈现器的图形 DDI 函数。 这些图形 DDI 函数帮助 GDI 绘制打印作业的页面图像。

呈现器程序还负责将文本呈现图像数据，以及打印机命令序列发送到打印后台处理程序，然后将定向数据流和命令指向打印机硬件。

可以通过提供修改 Pscript 的呈现操作[呈现插件](rendering-plug-ins.md)，标题部分中所述[自定义 Microsoft 的打印机驱动程序](customizing-microsoft-s-printer-drivers.md)。

 

 




