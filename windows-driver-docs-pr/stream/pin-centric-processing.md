---
title: 以引脚为中心的处理
description: 以引脚为中心的处理
ms.assetid: 0b6a02c2-e672-4568-a890-491c721ec3a7
keywords:
- pin 中心筛选器 WDK AVStream
- AVStream 针中心筛选器 WDK
- 筛选器类型 WDK AVStream
- AVStrMiniPinProcess
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa3f79da7d719ccd66da31197e77ce526b3b7ec7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823754"
---
# <a name="pin-centric-processing"></a>以引脚为中心的处理





编写 AVStream 微型驱动程序时，需要提供使用两种处理模式之一的筛选器：以零为中心的处理或以[筛选为中心的处理](filter-centric-processing.md)。

以引脚为中心的处理意味着当新帧到达 pin 队列时，AVStream 会调用微型驱动程序的 pin 进程调度例程。

以筛选为中心的处理意味着，当每个实例化的 pin 上有可用的数据帧时，AVStream 将调用微型驱动程序的筛选器进程调度例程。 请注意，这些定义指定默认行为;微型驱动程序可以通过在[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构中设置标志来修改默认行为。

一般而言，软件筛选器使用以筛选器为中心的处理和硬件筛选器使用以零为中心的处理。 例如，转换或呈现数据的硬件可以在以 pin 为中心的筛选器上路由数据。 在极少数情况下，可能会反转这些角色。

为了提供以 pin 为中心的筛选器，微型驱动程序提供了指向每个[**KSPIN\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)结构中*AVStrMiniPinProcess*回调例程的指针;请勿在[**KSFILTER\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)结构中提供处理调度。

如果微型驱动程序不在 KSPIN\_描述符中修改标志设置\_EX 结构，则 AVStream 将在三种情况下调用供应商提供的[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)回调例程：

-   Pin 会转换为最小处理状态。 帧必须已存在于队列中，并且 pin 必须从最小处理状态转换为至少最小处理状态。

-   新帧到达。 Pin 必须处于至少最小处理状态，并且在前导边缘或其前面不能有帧。

-   微型驱动程序显式调用[**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)。

默认情况下，暂停是最小处理状态。

此外，如果 pin 和门已关闭，AVStream 不会调用 pin 处理调度。 例如，如果使用**KSGATE**_Xxx_例程将额外的输入添加到 pin 的和入口，则不会调用进程调度。

当 AVStream 调用*AVStrMiniPinProcess*时，它提供指向具有可用数据的 pin 对象的指针。 然后，微型驱动程序的处理调度可以通过调用[**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)来获取[前导边缘指针](leading-and-trailing-edge-stream-pointers.md)。 然后，微型驱动程序使用[流指针](stream-pointers.md)API 操作流数据。

当 AVStream 调用*AVStrMiniPinProcess*调度时，使用以微型驱动程序为中心的处理的可以通过在相关[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构中设置标志来修改。 KSPIN\_描述符\_EX 参考页上的标志说明特别适用于实现以针为中心的筛选器的供应商。

如果微型驱动程序通过[**KsPinAcquireProcessingMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinacquireprocessingmutex)持有[处理互斥体](processing-mutex-in-avstream.md)，处理尝试可能会失败。 如果微型驱动程序通过使用**KSGATE** _\*_ 调用直接操作入口，则也可能会出现问题。

Windows 驱动程序工具包示例中的[AVStream 模拟硬件示例驱动程序（AVSHwS）](https://go.microsoft.com/fwlink/p/?linkid=256083)是用于模拟硬件的以 pin 为中心的捕获驱动程序。 Avshws 示例演示如何[通过 AVStream 实现 DMA](avstream-dma-services.md)。

 

 




