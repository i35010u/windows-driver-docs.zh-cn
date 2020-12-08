---
title: 在 64 位 Windows 中执行 DMA
description: 在 64 位 Windows 中执行 DMA
keywords:
- 64位 WDK 内核，将驱动程序移植到
- 将驱动程序移植到64位 Windows
- DMA 传输 WDK 内核，64位 Windows
- 双缓冲 WDK 64 位
- 直接内存访问 WDK 内核
- 多态性 WDK 64 位
- 数据结构 WDK 64 位
- 无符号操作 WDK 64 位
- 签名操作 WDK 64 位
- 指针算法 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d7301cece2bf177f088e2393cace3b09db118c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836911"
---
# <a name="performing-dma-in-64-bit-windows"></a>在 64 位 Windows 中执行 DMA





向驱动程序添加64位寻址支持可以显著提高系统的整体性能。 对于 (DMA) 执行直接内存访问的设备驱动程序，这一点特别重要。 在64位 Microsoft Windows 中，执行 DMA 但不支持64位寻址的设备驱动程序会双缓冲，从而降低相对性能。

尽管双缓冲通常会对 8 GB 系统 (单百分比点) 的影响较小，但这足以影响 i/o 密集型任务，如数据库活动。 随着物理内存量的增加，这一负面的性能影响也会随之增加。

为了支持64位 DMA，驱动程序应遵循以下准则：

1.  使用 **物理 \_ 地址** 结构来计算物理地址。

2.  将整个64位地址视为有效的物理地址。 例如，驱动程序不应对锁定的缓冲区调用 [**MmGetPhysicalAddress**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress) ，丢弃高32位，并将截断的地址传递到32位组件适配器。 这会导致内存损坏、i/o 中断和系统故障。

3.  使用 Windows 2000 中添加的高性能分散/收集例程 ([**GetScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list) 和 [**PutScatterGatherList**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)) 。

4.  检查 [**Mm64BitPhysicalAddress**](mm64bitphysicaladdress.md) 全局系统变量的值。 如果为 **TRUE**，则系统支持64位物理寻址。

5.  将 [**设备 \_ 描述**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)结构的 **Dma64BitAddresses** 成员设置为 **TRUE** ，以指示你的驱动程序支持64位 DMA 地址。

32位 Windows 中的 DMA 例程是64位就绪。 如果设备驱动程序正确使用这些例程，则 DMA 代码应在64位 Windows 上无需修改的情况下运行。

 

