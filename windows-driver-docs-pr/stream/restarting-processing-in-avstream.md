---
title: 在 AVStream 中重启处理
description: 在 AVStream 中重启处理
ms.assetid: f60d4dbd-61e6-4ae2-aa43-9edc8f36c3ff
keywords:
- 重新启动 AVStream 处理
- 重新启动 WDK AVStream 过程
- 继续处理 WDK AVStream
- 挂起状态 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e85951391c8f558dbca25412777062e25b6f960
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385684"
---
# <a name="restarting-processing-in-avstream"></a>在 AVStream 中重启处理





AVStream 停止处理如果任意下列条件为 true:

-   在 pin 为中心的环境中，不 pin 上当前可用的数据。

-   在筛选器为中心的环境中，至少一个固定为其**标志**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构却不设置 KSPIN\_标志\_帧\_不\_必需\_为\_处理，不具有等待处理的数据。 默认情况下，未设置此标志。

-   微型驱动程序的处理调度回调例程将返回状态\_PENDING，而不考虑帧可用性。 请注意处理调度可以是[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)或[ *AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)，具体取决于微型驱动程序实现[pin 以中心处理](pin-centric-processing.md)或[筛选器以中心处理](filter-centric-processing.md)。

AVStream 启动处理新数据到达到先前为空队列时。 因此，如果微型驱动程序的处理调度返回状态\_挂起时相关联的队列已满，微型驱动程序将永远不会调用到恢复处理。 如果状态的微型驱动程序设置\_挂起，微型驱动程序必须调用[ **KsPinAttemptProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattemptprocessing)或[ **KsFilterAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfilterattemptprocessing)恢复处理。

不会返回状态\_成功从处理调度如果微型驱动程序不会实际处理数据。 这将导致 AVStream 立即调用微型驱动程序，从而导致无限循环之间 AVStream 和处理调度。

 

 




