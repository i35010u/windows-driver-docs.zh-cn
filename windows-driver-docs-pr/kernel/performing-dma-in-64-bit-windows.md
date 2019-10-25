---
title: 在 64 位 Windows 中执行 DMA
description: 在 64 位 Windows 中执行 DMA
ms.assetid: 3ef00c05-356d-488a-8422-503d8132344d
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
ms.openlocfilehash: 5f9799487705dce1f7ac1d0354179197bcdf5499
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827711"
---
# <a name="performing-dma-in-64-bit-windows"></a>在 64 位 Windows 中执行 DMA





向驱动程序添加64位寻址支持可以显著提高系统的整体性能。 对于执行直接内存访问（DMA）的设备驱动程序，这一点特别重要。 在64位 Microsoft Windows 中，执行 DMA 但不支持64位寻址的设备驱动程序会双缓冲，从而降低相对性能。

虽然双缓冲在 8 GB 系统上通常会产生相对较小的影响（单百分比点），但这足以影响 i/o 密集型任务，如数据库活动。 随着物理内存量的增加，这一负面的性能影响也会随之增加。

为了支持64位 DMA，驱动程序应遵循以下准则：

1.  使用**物理\_地址**结构进行物理地址计算。

2.  将整个64位地址视为有效的物理地址。 例如，驱动程序不应对锁定的缓冲区调用[**MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress) ，丢弃高32位，并将截断的地址传递到32位组件适配器。 这会导致内存损坏、i/o 中断和系统故障。

3.  使用 Windows 2000 中新增的高性能散播/聚集例程（[**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)和[**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)）。

4.  检查[**Mm64BitPhysicalAddress**](mm64bitphysicaladdress.md)全局系统变量的值。 如果为**TRUE**，则系统支持64位物理寻址。

5.  将[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)结构的**Dma64BitAddresses**成员设置为**TRUE** ，以指示你的驱动程序支持64位 DMA 地址。

32位 Windows 中的 DMA 例程是64位就绪。 如果设备驱动程序正确使用这些例程，则 DMA 代码应在64位 Windows 上无需修改的情况下运行。

 

 




