---
title: 框架 DMA 对象
description: 框架 DMA 对象
ms.assetid: a5073bb0-a8c9-49fc-b280-e781f9f9c256
keywords:
- DMA 操作 WDK KMDF，对象
- 总线主控 DMA WDK KMDF，对象
- DMA 启用程序对象 WDK KMDF
- DMA 事务对象 WDK KMDF
- 常见缓冲区对象 WDK KMDF
- framework 对象 WDK KMDF，DMA 对象
- 启用程序对象 WDK KMDF
- 事务对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 639a304265bac147a21804d1239b655c02922076
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184047"
---
# <a name="framework-dma-objects"></a>框架 DMA 对象


\[仅适用于 KMDF\]




为了处理基于框架的驱动程序中的总线主控和系统模式 DMA 操作，该框架提供了三个对象：

<a href="" id="dma-enabler-object"></a>**DMA 启用程序对象**  
使用框架的 DMA 启用码对象，驱动程序可以将框架的 DMA 支持用于特定设备。 驱动程序必须为其支持 DMA 操作的每个设备创建 DMA 启用程序对象。

<a href="" id="dma-transaction-object"></a>**DMA transaction 对象**  
框架的 DMA transaction 对象表示单个 DMA i/o 操作。 如果设备使用 DMA 执行请求的操作，则基于框架的驱动程序通常会为它收到的每个 i/o 请求创建 DMA transaction 对象。

<a href="" id="common-buffer-object"></a>**通用缓冲区对象**  
框架的通用缓冲区对象表示一种计算机内存区域，该区域由驱动程序和设备进行同时访问。 某些驱动程序在为 DMA 设备设置 i/o 操作时 [使用公用缓冲区](using-common-buffers.md) 。

有关这些对象导出的接口的信息，请参阅：

[框架 DMA 对象引用](/windows-hardware/drivers/ddi/wdfdmaenabler/)

[Framework 公用缓冲区对象引用](/windows-hardware/drivers/ddi/wdfcommonbuffer/)

 

