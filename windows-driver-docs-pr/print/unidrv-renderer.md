---
title: Unidrv 渲染器
description: Unidrv 渲染器
keywords:
- Unidrv，呈现器
- 呈现器 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be4c90d4a500f2043d7166a71ec8f7cb1b474dd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835477"
---
# <a name="unidrv-renderer"></a>Unidrv 渲染器





Unidrv 呈现器作为 [打印机图形 DLL](printer-graphics-dll.md) 实现，因此，导出由 Microsoft 设备驱动程序接口定义的函数， (DDI) 用于图形驱动程序。 当应用程序调用图形设备接口 (GDI) 函数将图像发送到打印机设备时，内核模式图形引擎将调用呈现器的图形 DDI 函数。 这些图形 DDI 函数有助于在绘图打印作业的页面图像时使用 GDI。

呈现器还负责将呈现的图像数据以及打印机命令序列发送到打印后台处理程序，然后将映像和命令定向到打印机硬件。 呈现器发送的打印机命令在 [Unidrv 微型驱动程序](unidrv-minidrivers.md)中指定。

可以通过提供 [呈现插件](rendering-plug-ins.md)来修改 Unidrv 的呈现操作。

 

 




