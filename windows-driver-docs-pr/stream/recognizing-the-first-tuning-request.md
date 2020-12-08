---
title: 识别第一个调谐请求
description: 识别第一个调谐请求
keywords:
- 首次优化时请求 WDK 视频捕获
- 识别首次优化请求 WDK 视频捕获
- 收音机调谐器 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65d006d4945118e5f59790f58c7c27059a7da23b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839855"
---
# <a name="recognizing-the-first-tuning-request"></a>识别第一个调谐请求


某些调谐器需要 slewing，以获取有效的信号强度/PLL 信息，因此微型驱动程序可能需要在 *KsTvTune.ax* 发出初始优化请求时进行识别。

每个优化请求实际上是一对微型驱动程序的请求。 微型驱动程序首先接收一组 [**KSPROPERTY \_ 调谐器 \_ FREQUENCY**](./ksproperty-tuner-frequency.md) 请求，后跟一个或多个 get [**KSPROPERTY \_ 调谐器 \_ 状态**](./ksproperty-tuner-status.md) 请求。

在第一个优化请求中，在设置请求和第一个 get 请求之间存在延迟。 微型驱动程序设置 [**KSPROPERTY \_ 调谐器 \_ 模式 \_ Cap \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构的 **SettlingTime** 成员的延迟时间（以毫秒为单位）。 Get 请求每5毫秒重复一次，而 [**KSPROPERTY \_ 调谐器 \_ 状态 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)结构的 **繁忙** 成员不为零，最多可尝试5次。

*KsTvTune.ax* 在从设备收到 nonbusy 状态之前，或如果设备在 [**KSPROPERTY \_ 调谐器 \_ 模式 \_ cap \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构的 **SettlingTime** 成员指定的时间间隔后仍处于繁忙状态，则不会将优化请求视为已完成。

此后，在微调模式下，对于每个优化请求，都将在集请求和第一个 get 请求之间出现五毫秒的间隔。

如果你希望 *KsTvTune.ax* 在初始请求后至少重试一次，则在第一个优化请求上始终返回 **PLLOffset** 值1。 *KsTvTune.ax* 会立即尝试下一步，如 [**KSPROPERTY \_ 调谐器 \_ 模式 \_ 上限 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构的 **TuningGranularity** 成员指定的那样。 此时，如果微型驱动程序确定没有信号，则返回大于1或小于-1 的 **PLLOffset** 值; 如果微型驱动程序确定信号良好，则返回 **PLLOffset** 值-1 或0。

 

