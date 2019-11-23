---
title: 处理器数量的更改
description: 处理器数量的更改
ms.assetid: 9ced4b42-c83d-49da-8405-b95b0c0144fa
keywords:
- 动态硬件分区 WDK，更改处理器数量
- 硬件分区 WDK 动态，更改处理器数量
- 将 WDK 动态硬件分区，更改处理器数量
- 活动处理器 WDK 动态硬件分区
- 处理器计数 WDK 动态硬件分区
- 处理器关联 WDK 动态硬件分区
- 每处理器数据结构 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a39ae1e5c04ef14e72a3e4b1809d0a35727f4319
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828546"
---
# <a name="changes-to-the-number-of-processors"></a>处理器数量的更改


在动态分区的服务器上，可以随时将处理器添加到硬件分区。 因此，不应对硬件分区中活动处理器的数量、处理器关联值或分配给每个活动处理器的处理器编号作出任何假设。 在 "处理器关联值" 中设置的位表示硬件分区中当前活动的每个处理器。 如果将处理器添加到硬件分区，则设置的特定位将会更改。

如果下列任何陈述对于设备驱动程序都是正确的，则必须更新驱动程序，以便在将处理器动态添加到硬件分区时，它将在动态分区服务器上正常运行：

-   设备驱动程序使用硬件分区中活动处理器的数量来确定它所使用的资源量，如它所分配的内存量、它创建的线程数或它使用的其他资源量。 在这种情况下，如果将处理器动态添加到硬件分区，则设备驱动程序的资源分配将不正确。 这可能会对驱动程序的性能或行为产生负面影响。

-   设备驱动程序会遍历处理器关联值的位数。 在这种情况下，如果设备驱动程序无法处理对处理器关联值的动态更改，或者无法处理所设置的位序列中的间隔，则设备驱动程序可能无法正常工作。

-   设备驱动程序使用处理器关联值中的位将已分配给驱动程序的资源分配给特定处理器。 在这种情况下，如果将处理器动态添加到硬件分区，则设备驱动程序的资源分配将不正确。 这可能会对驱动程序的性能或行为产生负面影响。

-   设备驱动程序为硬件分区中的每个活动处理器分配数据结构。 在这种情况下，如果尝试访问动态添加到硬件分区的处理器的这些数据结构，则设备驱动程序可能会导致不良行为、数据损坏或 bug 检查发生。

-   设备驱动程序的调度例程使用其上运行的处理器的处理器号来访问分配给该特定处理器的数据结构或其他资源。 在这种情况下，如果设备驱动程序的调度例程尝试访问已动态添加到硬件分区的处理器的这些资源，则可能会导致不良行为、数据损坏或 bug 检查。

-   设备驱动程序计划其中断服务例程（Isr）、延迟的过程调用（Dpc）或特定处理器上的其他线程。 在这种情况下，如果将处理器添加到硬件分区，则设备驱动程序可能会停止正常工作，并且设备驱动程序将无法完全使用任何新处理器。

-   设备驱动程序不支持资源重新平衡。 在这种情况下，设备驱动程序将无法使用添加到硬件分区的任何新处理器来处理中断。

-   设备驱动程序使用负载平衡算法跨多个处理器分发 i/o 请求的处理。 在这种情况下，如果将处理器添加到硬件分区，则设备驱动程序可能会停止正常工作，并且设备驱动程序将无法完全使用任何新处理器。

如果设备驱动程序受到活动处理器数量的更改的影响，则它必须向操作系统注册自身，以便在将处理器添加到硬件分区时收到通知。 当设备驱动程序得到通知时，它可以根据需要对安全和最佳操作做出响应。 有关设备驱动程序如何向操作系统注册自身的详细信息，请参阅[驱动程序通知](driver-notification.md)。

若要检索硬件分区中活动处理器的当前数量，设备驱动程序应调用[**KeQueryActiveProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryactiveprocessorcount)函数。 若要检索当前的处理器关联值，设备驱动程序可调用[**KeQueryActiveProcessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryactiveprocessors)函数或**KeQueryActiveProcessorCount**函数。

**请注意**  如果设备驱动程序为硬件分区中的每个活动处理器分配数据结构，并且如果为新处理器的数据结构分配内存失败，则设备驱动程序将会失败，并且设备驱动程序在驱动程序初始化期间可以分配足够的这些数据结构来处理操作系统支持的处理器的最大数量。 在这种情况下，在将新处理器添加到硬件分区时，设备驱动程序将不必分配新的数据结构。 但是，除非这些数据结构的大小非常小，否则内存资源的使用效率会降低。 设备驱动程序可以通过调用[**KeQueryMaximumProcessorCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerymaximumprocessorcount)函数来查询操作系统支持的处理器的最大数量。

 

**重要**  设备驱动程序在通知已将处理器添加到硬件分区时，应始终更新所有已保存的活动处理器数和处理器关联值。

 

**重要**  设备驱动程序不应计算处理器关联值中的设置位数，以确定硬件分区中活动处理器的数目。 建议设备驱动程序调用**KeQueryActiveProcessorCount**函数以实现此目的。 此函数返回活动处理器的数量和关联的处理器关联值。

 

**重要**  为 windows Vista、windows Server 2008 及更高版本的 windows 构建的设备驱动程序不得使用[**KeNumberProcessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryactiveprocessors)内核变量来确定硬件分区中活动处理器的数量。 Windows Vista Service Pack 1 （SP1）、Windows Server 2008 和更高版本的 Windows 中的**KeNumberProcessors**内核变量已过时。

 

 

 




