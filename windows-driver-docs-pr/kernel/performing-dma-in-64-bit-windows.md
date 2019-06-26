---
title: 在 64 位 Windows 中执行 DMA
description: 在 64 位 Windows 中执行 DMA
ms.assetid: 3ef00c05-356d-488a-8422-503d8132344d
keywords:
- 64 位 WDK 内核，移植到驱动程序
- 移植到 64 位 Windows 的驱动程序
- DMA 传输 WDK 内核，64 位 Windows
- 双缓冲 WDK 64 位
- 直接内存访问 WDK 内核
- 多态性 WDK 64 位
- 数据结构 WDK 64 位
- WDK 64 位无符号的操作
- 签名的操作 WDK 64 位
- 指针算术 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cfd18a1efdfbc9c7d5853d515eff78ae4a98d51
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384740"
---
# <a name="performing-dma-in-64-bit-windows"></a>在 64 位 Windows 中执行 DMA





将 64 位寻址支持添加到您的驱动程序可以显著提高总体系统性能。 这一点尤其重要的执行直接内存访问 (DMA) 的设备驱动程序。 在 64 位 Microsoft Windows 设备驱动程序执行 DMA 但不是支持 64 位寻址是双缓冲，这会导致较低的相对性能。

尽管双缓冲通常在 8 GB 的系统上具有相对较小的影响 （一个百分比磅为单位），但这就足以影响 O 密集型任务，例如数据库活动。 物理内存增加的量，这种负面性能影响也将增加。

若要支持 64 位 DMA，驱动程序应遵守以下准则：

1.  使用**物理\_地址**物理地址计算的结构。

2.  将整个的 64 位地址视为有效的物理地址。 例如，驱动程序不应调用[ **MmGetPhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmgetphysicaladdress)锁定缓冲区，放弃高 32 位，并将被截断的地址传递给 32 位组件适配器。 这会导致损坏的内存、 I/O 丢失和系统故障。

3.  使用高性能散播-聚集例程 ([**GetScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_scatter_gather_list)并[ **PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_scatter_gather_list)) 中添加Windows 2000。

4.  检查的值[ **Mm64BitPhysicalAddress** ](mm64bitphysicaladdress.md)全局系统变量。 如果它是 **，则返回 TRUE**，系统支持 64 位物理寻址。

5.  设置**Dma64BitAddresses**的成员[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)结构**TRUE**以指示你驱动程序支持 64 位 DMA 地址。

32 位 Windows 中的 DMA 例程是 64 位就绪。 如果您的设备驱动程序正确使用这些例程，DMA 代码应无需修改即可在 64 位 Windows。

 

 




