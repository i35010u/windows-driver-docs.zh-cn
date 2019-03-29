---
title: Unidrv 渲染器
description: Unidrv 渲染器
ms.assetid: 5c19eb9c-149b-4587-a12d-f01164231b51
keywords:
- Unidrv、 呈现器
- 呈现器 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 757707092f723c9a93b3bd2b08a91bb5497510a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568405"
---
# <a name="unidrv-renderer"></a>Unidrv 渲染器





Unidrv 呈现器作为[打印机图形 DLL](printer-graphics-dll.md) ，并因此将导出定义由 Microsoft 设备驱动程序接口 (DDI) 的图形驱动程序的函数。 当应用程序调用图形设备接口 (GDI) 函数将映像发送到打印机设备时，内核模式图形引擎会调用呈现器的图形 DDI 函数。 这些图形 DDI 函数帮助 GDI 绘制打印作业的页面图像。

程序还负责发送呈现器呈现图像数据，以及打印机命令序列，打印后台处理程序，后者随后将定向映像和命令指向打印机硬件。 呈现器发送的打印机命令中指定[Unidrv 微型驱动程序](unidrv-minidrivers.md)。

可以通过提供修改 Unidrv 的呈现操作[呈现插件](rendering-plug-ins.md)。

 

 




