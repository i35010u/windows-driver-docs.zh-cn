---
title: 在 AVStream 中重启处理
description: 在 AVStream 中重启处理
ms.assetid: f60d4dbd-61e6-4ae2-aa43-9edc8f36c3ff
keywords:
- 正在重启 AVStream 处理
- AVStream 进程重新启动 WDK
- 继续处理 WDK AVStream
- 挂起状态 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86512a0879a42fd8e30e57a902bf36a1e53e8722
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186319"
---
# <a name="restarting-processing-in-avstream"></a>在 AVStream 中重启处理





如果满足以下任一条件，AVStream 将停止处理：

-   在以 pin 为中心的环境中，当前没有数据可用于 pin。

-   在以筛选为中心的环境中，至少有一个[**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的**Flags**成员未设置 \_ 用于处理的 KSPIN 标记帧的 pin \_ \_ \_ \_ \_ ，也就是没有数据等待处理。 默认情况下，不设置此标志。

-   微型驱动程序的处理调度回调例程返回状态 \_ "挂起"，而不考虑帧的可用性。 请注意，处理调度可以是 [*AVStrMiniFilterProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess) 或 [*AVStrMiniPinProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)，具体取决于微型驱动程序是否实现以 [零为中心的处理](pin-centric-processing.md) 或以 [筛选为中心的处理](filter-centric-processing.md)。

当新数据到达之前的空队列时，AVStream 启动处理。 因此，如果在关联的队列已满时微型驱动程序的处理调度返回 "挂起" 状态 \_ ，则永远不会调用微型驱动程序来继续处理。 如果微型驱动程序将状态设置 \_ 为 "挂起"，则微型驱动程序必须调用 [**KsPinAttemptProcessing**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing) 或 [**KsFilterAttemptProcessing**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterattemptprocessing) 才能恢复处理。

\_如果微型驱动程序不实际处理数据，则不会从处理调度返回状态 SUCCESS。 这会导致 AVStream 再次调用微型驱动程序，从而导致 AVStream 与处理调度之间出现无限循环。

 

