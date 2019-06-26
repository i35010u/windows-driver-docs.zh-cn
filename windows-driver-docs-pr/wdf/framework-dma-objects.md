---
title: 框架 DMA 对象
description: 框架 DMA 对象
ms.assetid: a5073bb0-a8c9-49fc-b280-e781f9f9c256
keywords:
- DMA 操作 WDK KMDF，对象
- 主总线 DMA WDK KMDF 对象
- DMA 促成因素对象 WDK KMDF
- DMA 事务对象 WDK KMDF
- 常见的缓冲区对象 WDK KMDF
- framework 对象 WDK KMDF，DMA 对象
- 启用程序对象 WDK KMDF
- 事务对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d8c02e326586d098c4e85c2b1b89091c6dc850
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368680"
---
# <a name="framework-dma-objects"></a>框架 DMA 对象


\[仅适用于 KMDF\]




若要处理基于 framework 的驱动程序中的总线 master 和系统模式 DMA 操作，framework 提供了三个对象：

<a href="" id="dma-enabler-object"></a>**DMA 启用程序对象**  
框架的 DMA 促成因素对象使框架的 DMA 支持用于特定设备的驱动程序。 该驱动程序必须为每个支持 DMA 操作其设备创建 DMA 推动器对象。

<a href="" id="dma-transaction-object"></a>**DMA 事务对象**  
框架的 DMA 事务对象表示单个 DMA I/O 操作。 基于框架的驱动程序通常创建接收，每个 I/O 请求的 DMA 事务对象，如果设备使用 DMA 来执行请求的操作。

<a href="" id="common-buffer-object"></a>**常见的缓冲区对象**  
框架的常见缓冲区对象表示映射，可同时访问驱动程序和设备的计算机内存的区域。 某些驱动程序[使用常见缓冲区](using-common-buffers.md)时设置 DMA 的设备的 I/O 操作。

有关这些对象将导出的接口的信息，请参阅：

[Framework DMA 对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/)

[Framework 常见缓冲区对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcommonbuffer/)

 

 





