---
title: 识别第一个调谐请求
description: 识别第一个调谐请求
ms.assetid: dc18a056-16f8-4b99-97e3-52c92464a2b2
keywords:
- 第一个优化请求 WDK 视频捕获
- 识别第一次优化请求 WDK 视频捕获
- 广播调谐器 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4cc6b83018a018b53f2fbb524f29985a2ecc62a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366498"
---
# <a name="recognizing-the-first-tuning-request"></a>识别第一个调谐请求


某些调谐器需要围绕频率来获取有效的信号强度/PLL 信息，因此微型驱动程序可能需要识别何时回转*KsTvTune.ax*进行初始优化请求。

每个优化请求是实际的微型驱动程序的请求的对。 微型驱动程序第一次接收到一组[ **KSPROPERTY\_调谐器\_频率**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-frequency)跟一个或多个 get 请求[ **KSPROPERTY\_调谐器\_状态**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status)请求。

第一次优化请求，有很集请求与第一个 get 请求之间的延迟。 微型驱动程序设置 （毫秒） 中的延迟长度**SettlingTime**的成员[ **KSPROPERTY\_调谐器\_模式\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构。 重复的 get 请求时每隔五个毫秒**忙**的成员[ **KSPROPERTY\_调谐器\_状态\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)结构为非零值，最多 5 次尝试。

*KsTvTune.ax*不考虑优化请求完成直到 nonbusy 状态收到来自该设备，或如果该设备是由指定的时间间隔后仍忙于 20 毫秒**SettlingTime**的成员[ **KSPROPERTY\_调谐器\_模式\_CAPS\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构，具体取决于第一个。

此后，每个优化请求在微调模式期间，集请求之间将有五个毫秒时间间隔内，而第一个 get 请求。

如果你想*KsTvTune.ax*若要重试初始请求后的至少一次，始终返回**PLLOffset** 1 第一次优化请求的值。 *KsTvTune.ax*更高版本，由指定的下一步会立即尝试**TuningGranularity**的成员[ **KSPROPERTY\_调谐器\_模式\_CAPS\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构。 此时，你可能会返回**PLLOffset**值大于 1 或小于-1 如果你的微型驱动程序确定没有信号，或**PLLOffset** -1 或 0，如果你的微型驱动程序确定的值信号是很好。

 

 




