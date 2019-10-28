---
title: 识别第一个调谐请求
description: 识别第一个调谐请求
ms.assetid: dc18a056-16f8-4b99-97e3-52c92464a2b2
keywords:
- 首次优化时请求 WDK 视频捕获
- 识别首次优化请求 WDK 视频捕获
- 收音机调谐器 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f728c94ae3286224d5c8725d932ed902c9a3be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841660"
---
# <a name="recognizing-the-first-tuning-request"></a>识别第一个调谐请求


某些调谐器需要 slewing，以获取有效的信号强度/PLL 信息，因此微型驱动程序可能需要在*KsTvTune.ax*发出初始优化请求时进行识别。

每个优化请求实际上是一对微型驱动程序的请求。 微型驱动程序首先收到 set [**KSPROPERTY\_调谐器\_FREQUENCY**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-frequency)请求，后跟一个或多个 get [**KSPROPERTY\_调谐器\_状态**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status)请求。

在第一个优化请求中，在设置请求和第一个 get 请求之间存在延迟。 微型驱动程序以毫秒为单位设置[**KSPROPERTY\_调谐器\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)**的延迟**时间长度（以毫秒为单位）\_cap\_S 结构。 Get 请求每隔五毫秒重复一次，而 KSPROPERTY\_调谐器的**繁忙**成员[ **\_状态\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)结构为非零，最多尝试5次。

*KsTvTune.ax*在从设备收到 nonbusy 状态之前，或如果设备在\_KSPROPERTY 的**SettlingTime**成员指定的间隔后仍处于繁忙状态，则不会将优化请求视为已完成。 [**调谐器\_模式\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构，以首先为准。

此后，在微调模式下，对于每个优化请求，都将在集请求和第一个 get 请求之间出现五毫秒的间隔。

如果你希望*KsTvTune.ax*在初始请求后至少重试一次，则在第一个优化请求上始终返回**PLLOffset**值1。 *KsTvTune.ax*会立即尝试下一步，如[**KSPROPERTY\_调谐器\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)的**TuningGranularity**成员指定\_cap\_S 结构。 此时，如果微型驱动程序确定没有信号，则返回大于1或小于-1 的**PLLOffset**值; 如果微型驱动程序确定信号良好，则返回**PLLOffset**值-1 或0。

 

 




