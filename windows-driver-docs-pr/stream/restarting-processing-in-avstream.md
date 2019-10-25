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
ms.openlocfilehash: f772fcee30e0d700014b93f184d47c27aae105dc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844952"
---
# <a name="restarting-processing-in-avstream"></a>在 AVStream 中重启处理





如果满足以下任一条件，AVStream 将停止处理：

-   在以 pin 为中心的环境中，当前没有数据可用于 pin。

-   在以筛选为中心的环境中，至少有一个\_KSPIN 的**标志**成员的 PIN [ **\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构未将 KSPIN\_标志设置\_的\_\_所需\_\_正在处理，没有数据等待处理。 默认情况下，不设置此标志。

-   微型驱动程序的处理调度回调例程返回状态\_"挂起"，与帧的可用性无关。 请注意，处理调度可以是[*AVStrMiniFilterProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)或[*AVStrMiniPinProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)，具体取决于微型驱动程序是否实现以[零为中心的处理](pin-centric-processing.md)或以[筛选为中心的处理](filter-centric-processing.md)。

当新数据到达之前的空队列时，AVStream 启动处理。 因此，如果微型驱动程序的处理调度返回状态\_当关联的队列已满时，将永远不会调用微型驱动程序来继续处理。 如果微型驱动程序将状态设置\_"挂起"，则微型驱动程序必须调用[**KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing)或[**KsFilterAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterattemptprocessing)才能恢复处理。

如果微型驱动程序不实际处理数据，则不会从处理调度返回状态\_成功。 这会导致 AVStream 再次调用微型驱动程序，从而导致 AVStream 与处理调度之间出现无限循环。

 

 




