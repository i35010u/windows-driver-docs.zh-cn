---
title: 使用无线电调谐器的视频捕获设备
description: 使用无线电调谐器的视频捕获设备
ms.assetid: 36e3ca98-cb1b-46cc-809a-8c9ad08a53c8
keywords:
- 广播调谐器 WDK 视频捕获
- PLL 偏移量 WDK 视频捕获
- 信号强度 WDK 视频捕获
- 手动单选优化 WDK 视频捕获
- 调频调谐器 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0516b11d079e4bdda6d2c03a9cf6dd4323f3764
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351602"
---
# <a name="video-capture-devices-with-radio-tuners"></a>使用无线电调谐器的视频捕获设备


Microsoft Windows XP 及更高版本，并包含 FM 的视频捕获设备单选调谐器 Microsoft DirectX 8.1 及更高版本提供支持。

使用带有调频调谐器设备视频捕获微型驱动程序应支持[ **KSPROPERTY\_调谐器\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff565921)属性。 这将允许用户模式下客户端检索[ **KSPROPERTY\_调谐器\_状态\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565925)结构描述的优化操作的进度。

微型驱动程序可以支持三种优化策略之一：

1.  **优化由 PLL 偏移量。**

    如果您调频广播的调谐器硬件支持优化通过 PLL 偏移量，你的微型驱动程序应设置**战略**的成员[ **KSPROPERTY\_调谐器\_模式\_CAP\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872) KS 结构\_调谐器\_策略\_PLL。

    如果您调频广播的调谐器硬件不提供 PLL 支持，微型驱动程序应模拟 PLL 支持通过使用本机信号强度指示符。 优化逻辑，系统提供 FM *KsTvTune.ax*微型驱动程序指定其支持的情况下，才会启用**KS\_调谐器\_策略\_PLL**策略。

2.  **优化的信号强度。**

    如果微型驱动程序设置**战略**KSPROPERTY 成员\_调谐器\_模式\_CAPS\_KS S 结构\_调谐器\_策略\_信号\_强度*KsTvTune.ax*仍尝试使用**PLLOffset** KSPROPERTY 成员\_调谐器\_状态\_S 结构。 因此，这不是将来的兼容性的有效选项。

    此外，微型驱动程序应设置**SignalStrength**的成员[ **KSPROPERTY\_调谐器\_状态\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565925)结构为-1、 0 或 1，具体取决于是否当前选定的可接受的频率。 供应商决定哪些接收方信号强度指示符 (RSSI) 或分贝 millivolt (dBmV) 级别高于或低于基线电压构成 FM 接收的可接受信号。

3.  **微型驱动程序通过手动执行优化。**

    设置**战略**的成员[ **KSPROPERTY\_调谐器\_模式\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872) 结构**KS\_调谐器\_策略\_驱动程序\_优化**控制优化微型驱动程序中的逻辑。

在 FM 模式下， *KsTvTune.ax* 200 kHz 带区周围的频率 (任意一侧为 100 kHz)，介绍了如何使用微型驱动程序指定**TuningGranularity**的成员[ **KSPROPERTY\_调谐器\_模式\_CAP\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872)步骤大小的结构。 搜索将停止何时*KsTvTune.ax*已搜索整个 200khz 带区，或微型驱动程序确定，良好的信号已找到，以先发生者为准。

优化时间更长，如果微型驱动程序始终指定**PLLOffset**值为-1 或 1。 在此情况下中的优化逻辑*KsTvTune.ax*重试频率范围重叠。 微型驱动程序应指定**PLLOffset**为-1 或 1 仅在第一个优化请求，或当内最佳的信号的八个步骤时调谐器。 有关优化请求的详细信息请参阅[识别的第一个优化请求](recognizing-the-first-tuning-request.md)。

优化过程始终根据应用程序的请求启动的中心频率，并不高于中央上方 100 kHz 步骤。 但是，如果**PLLOffset**成为 1 近 100 kHz 的上限，超出 100 kHz 外优化的逻辑步骤。

如果优化过程中的上限范围未找到可接受的信号，它将尝试下面的中心频率，单步执行从不低于 100 kHz 下面 center 和结束的中心频率，如果它仍找到没有可接受的信号。 同样，如果**PLLOffset**成为附近的中心频率，最后返回到它之前优化之外的中心频率的步骤 1。

一个**PLLOffset**成员值为-1 或 1 上的第一个优化请求的原因*KsTvTune.ax*进入微调模式。 微调模式下的包括优化步骤指定的时间间隔由请求中快速连续**TuningGranularity**的成员[ **KSPROPERTY\_调谐器\_模式\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872)方向中的结构由**PLLOffset**。

*KsTvTune.ax*停止其优化的尝试，如果后中增加或减少频率的八个微调步骤不成功。 之后*KsTvTune.ax*正在进行微调模式下，如果**PLLOffset**方向从-1 更改为 1 或为-1，1 或 0，优化请求被视为成功。 进行微调和通过 200khz 带搜索停止在该点。

但是，如果**PLLOffset**大于 1 或小于-1，微调未启动，或者放弃。 尽管两者都使用指定中的步大小，微调模式是独立于通过 200khz 带区周围的中心频率，搜索**TuningGranularity** (因此始终返回对警告**PLLOffset**为-1..1)。

 

 




