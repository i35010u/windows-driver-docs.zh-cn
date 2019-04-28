---
title: DMA 事务和 DMA 传输
description: DMA 事务和 DMA 传输
ms.assetid: afcbe756-1a45-410b-8260-2c2c611e6a70
keywords:
- DMA 事务 WDK KMDF
- DMA 操作 WDK KMDF，事务
- 主总线 DMA WDK KMDF 事务
- DMA 操作 WDK KMDF 传输
- 主总线 DMA WDK KMDF 传输
- DMA 传输 WDK KMDF
- DMA 事务 WDK KMDF 关于 DMA 事务
- DMA 将 WDK KMDF 传输有关 DMA 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38b52b071fc939380b40b9c386798088f95ab348
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327871"
---
# <a name="dma-transactions-and-dma-transfers"></a>DMA 事务和 DMA 传输


\[仅适用于 KMDF\]




若要了解 framework 如何处理总线 master 和系统模式 DMA 操作，您必须知道以下两个术语：

<a href="" id="dma-transaction"></a>**DMA 事务**  
DMA 事务是一个完整的 I/O 操作，如单个读取或写入请求与应用程序。

<a href="" id="dma-transfer"></a>**DMA 传输**  
DMA 传输是将数据传输到设备的计算机内存或从设备到计算机内存的单个硬件操作。

单个 DMA 事务始终包含至少一个 DMA 传输，但事务可以包含多个传输。

当基于 framework 的驱动程序收到的 I/O 请求时，该驱动程序通常创建单个 DMA 事务对象来表示该请求。 当框架开始维护事务时，它确定设备可以处理单个传输中的整个事务。 如果事务而言太大，框架会将多个传输到该事务。

 

 





