---
title: DMA 事务和 DMA 传输
description: DMA 事务和 DMA 传输
keywords:
- DMA 事务 WDK KMDF
- DMA 操作 WDK KMDF，事务
- 总线主控 DMA WDK KMDF，事务
- DMA 操作 WDK KMDF，传输
- 总线主控 DMA WDK KMDF，传输
- DMA 传输 WDK KMDF
- DMA 事务 WDK KMDF，关于 DMA 事务
- DMA 传输 WDK KMDF，关于 DMA 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c772be75577701c96c8465da931f73648310fd78
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814825"
---
# <a name="dma-transactions-and-dma-transfers"></a>DMA 事务和 DMA 传输


\[仅适用于 KMDF\]




若要了解框架如何处理总线主操作和系统模式 DMA 操作，必须了解以下两个术语：

<a href="" id="dma-transaction"></a>**DMA 事务**  
DMA 事务是一个完整的 i/o 操作，例如应用程序的单个读取或写入请求。

<a href="" id="dma-transfer"></a>**DMA 传输**  
DMA 传输是单个硬件操作，用于将数据从计算机内存传输到设备或从设备传输到计算机内存。

单个 DMA 事务始终包含至少一个 DMA 传输，但一个事务可包含多个传输。

当基于框架的驱动程序收到 i/o 请求时，驱动程序通常会创建一个 DMA 事务对象来表示请求。 当框架开始为事务提供服务时，它确定设备是否可以在单个传输中处理整个事务。 如果事务太大，则该框架会将事务分为多个传输。

 

 





