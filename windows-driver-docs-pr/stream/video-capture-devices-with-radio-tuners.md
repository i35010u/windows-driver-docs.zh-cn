---
title: 使用无线电调谐器的视频捕获设备
description: 使用无线电调谐器的视频捕获设备
ms.assetid: 36e3ca98-cb1b-46cc-809a-8c9ad08a53c8
keywords:
- 收音机调谐器 WDK 视频捕获
- PLL 偏移 WDK 视频捕获
- 信号强度 WDK 视频捕获
- 手动收音机调谐 WDK 视频捕获
- 调频广播音频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee80453a2bfbb8dafb93b79a67ee9307fc68990
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844936"
---
# <a name="video-capture-devices-with-radio-tuners"></a>使用无线电调谐器的视频捕获设备


Microsoft Windows XP 和更高版本以及 Microsoft DirectX 8.1 和更高版本提供对包含调频收音机调谐器的视频捕获设备的支持。

对于带有调频调谐器的设备，视频捕获微型驱动程序应支持[**KSPROPERTY\_调谐器\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-status)属性。 这将允许用户模式客户端检索[**KSPROPERTY\_调谐器\_状态\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)结构，该结构描述优化操作的进度。

微型驱动程序可以支持以下三种优化策略之一：

1.  **通过 PLL 偏移量进行调整。**

    如果调频调谐器硬件支持通过 PLL 偏移量优化，则微型驱动程序应将[**KSPROPERTY\_调谐器\_\_\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)的**策略**成员设置为 KS\__9_ PLL.

    如果调频调谐器硬件未提供 PLL 支持，则微型驱动程序应通过使用本机信号强度指示器来模拟 PLL 支持。 仅当微型驱动程序指定它支持**KS\_调谐器\_策略\_PLL**策略时，才会启用系统提供的*KSTVTUNE.AX*中的 FM 优化逻辑。

2.  **按信号强度进行调整。**

    如果微型驱动程序将 KSPROPERTY\_\_调谐器的**战略**成员设置\_Cap\_S 结构到 KS\_调谐器\_策略\_信号\_强度， *KsTvTune.ax*仍尝试使用KSPROPERTY\_调谐器\_状态\_S 结构的**PLLOffset**成员。 因此，这并不是一个有效的选项，因此不能用于将来的兼容性。

    此外，微型驱动程序应将[**KSPROPERTY\_调谐器\_\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)的**SignalStrength**成员设置为-1、0或1，具体取决于当前是否选择了可接受的频率。 供应商决定高于或低于基线电压的接收方信号强度指示器（RSSI）或分贝 millivolt （dBmV）级别，这会为调频接收提供可接受的信号。

3.  **由微型驱动程序手动执行的优化。**

    将[**KSPROPERTY\_调谐器\_\_\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)的 "**策略**" 成员设置为 " **KS\_\_\_\_**

在 FM 模式下， *KsTvTune.ax*使用 [**KSPROPERTY\_调谐器\_模式\_\_下的微型驱动程序 TuningGranularity 成员，使用的成员（两侧 100 kHz）来逐步完成200**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)作为步长大小的结构。 当*KsTvTune.ax*搜索整个 200 kHz 带区，或微型驱动程序确定已找到良好的信号时（以先发生的为准），搜索将停止。

如果微型驱动程序始终将**PLLOffset**值指定为-1 或1，则优化需要更长时间。 在这种情况下， *KsTvTune.ax*中的优化逻辑将重试重叠的频率范围。 微型驱动程序应仅在第一个优化请求上指定**PLLOffset**或1，当调谐器处于最佳信号的8个步骤中时。 有关优化请求的详细信息，请参阅[识别首次优化请求](recognizing-the-first-tuning-request.md)。

根据应用程序的要求，优化过程始终以中心频率开始，并在中心上方向上提升 100 kHz。 但是，如果**PLLOffset**的值为1，接近 100-khz 的限制，则优化逻辑的步长超过100。

如果优化过程在上部范围内找不到可接受的信号，则它会尝试使用中心频率，从中心下面不低于 100 kHz 的位置向上进行，如果仍未找到可接受的信号，则从中心频率结束。 同样，如果**PLLOffset**在中心频率附近变为1，则在最终返回到它之前，将步骤调整到超出中心频率。

在第一个优化请求上， **PLLOffset**成员值为-1 或1将导致*KsTvTune.ax*进入微调模式。 微调模式按由[**KSPROPERTY\_调谐器\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)的**TuningGranularity**成员指定的单步执行的步骤间隔，按指定方向\_cap\_**PLLOffset**。

如果在增加或减少频率的8次微调步骤之后失败， *KsTvTune.ax*将停止其优化尝试。 *KsTvTune.ax*在微调模式下后，如果**PLLOffset**更改了从-1 到1的方向，或从1到-1，或变为0，则优化请求将视为成功。 此时，通过 200 kHz 的微调和搜索都会停止。

但是，如果**PLLOffset**大于1或小于-1，则不会开始微调，或者放弃。 尽管这两种模式都使用**TuningGranularity**中指定的步骤大小（这就会提醒始终返回-1 的**PLLOffset** ），但微调模式独立于在中心频率范围内搜索 200 kHz。

 

 




