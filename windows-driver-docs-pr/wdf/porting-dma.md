---
title: 移植 DMA
description: 移植 DMA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eae29d9d7c80ef88ee387b5223e8ef05daba1ab0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796361"
---
# <a name="porting-dma"></a>移植 DMA


\[仅适用于 KMDF\]

在 KMDF 驱动程序中执行 DMA (直接内存访问) 比 WDM 驱动程序更简单，因为框架代表驱动程序处理许多详细信息。

基本上，基于框架的驱动程序将创建一个 DMA 启用码对象，指定设备的 DMA 功能，并提供一个回调函数，该函数操纵硬件以执行传输。

框架确定传输所需的映射寄存器的数量，分配映射寄存器，生成散点/集合列表 (如果设备支持散播/聚集 DMA) ，并在必要时刷新处理器缓存和缓冲区。

有关实现的详细信息，请参阅 [在 KMDF 驱动程序中处理 DMA 操作](introduction-to-dma-in-windows-driver-framework.md)。

 

 





