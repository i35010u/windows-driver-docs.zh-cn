---
title: 移植 DMA
description: 移植 DMA
ms.assetid: 457B6459-EE02-4A2C-8D25-81CE1D9265DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a4a80036c48e6be4c073b5b70de2da4894ca226
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390101"
---
# <a name="porting-dma"></a>移植 DMA


\[仅适用于 KMDF\]

KMDF 驱动程序中执行 DMA （直接内存访问） 是比 WDM 驱动程序中更简单，因为该框架将处理许多代表该驱动程序的详细信息。

基本上，基于框架的驱动程序创建 DMA 启用程序对象、 指定的设备，DMA 功能并提供操作执行传输的硬件的回调函数。

框架确定所需的传输的映射寄存器的数量、 分配的映射寄存器、 生成散播-聚集列表 （如果设备支持散播-聚集 DMA），并刷新处理器缓存并根据需要随时的缓冲区。

有关实现的详细信息，请参阅[KMDF 驱动程序中处理 DMA 操作](handling-dma-operations-in-kmdf-drivers.md)。

 

 





