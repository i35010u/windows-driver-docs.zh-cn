---
title: 移植 DMA
description: 移植 DMA
ms.assetid: 457B6459-EE02-4A2C-8D25-81CE1D9265DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b30590da01a733b647b40f3cc4182f7679e887df
ms.sourcegitcommit: 057b72e8a44ba8f4282e072edc7be0b7e9341d2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412476"
---
# <a name="porting-dma"></a>移植 DMA


\[仅适用于 KMDF\]

在 KMDF 驱动程序中执行 DMA (直接内存访问) 比 WDM 驱动程序更简单，因为框架代表驱动程序处理许多详细信息。

基本上，基于框架的驱动程序将创建一个 DMA 启用码对象，指定设备的 DMA 功能，并提供一个回调函数，该函数操纵硬件以执行传输。

框架确定传输所需的映射寄存器的数量，分配映射寄存器，生成散点/集合列表 (如果设备支持散播/聚集 DMA) ，并在必要时刷新处理器缓存和缓冲区。

有关实现的详细信息，请参阅 [在 KMDF 驱动程序中处理 DMA 操作](introduction-to-dma-in-windows-driver-framework.md)。

 

 





