---
title: 采样频率的硬件约束
description: 采样频率的硬件约束
keywords:
- 示例频率约束 WDK 音频
- 限制采样频率 WDK 音频
- 硬件约束 WDK 音频
- 频率约束 WDK 音频
- 数据交集处理程序 WDK 音频，示例频率限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0a50e633734dda80f6df338ea1df2c3402e27b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786525"
---
# <a name="hardware-constraints-on-sample-frequency"></a>采样频率的硬件约束


## <span id="hardware_constraints_on_sample_frequency"></span><span id="HARDWARE_CONSTRAINTS_ON_SAMPLE_FREQUENCY"></span>


某些音频设备要求适配器筛选器接收器 pin 的采样频率与数字输出端口或麦克风的输入流的频率匹配。 例如，声霸卡16兼容硬件通常具有单个 crystal，这会限制其输入和输出流以相同的时钟速率运行。 对于其各个机载音频流可以支持多个时钟速率的适配器，可能仍需要将不同时钟速率的数目限制为某个较小的数字。

由于这些原因，适配器驱动程序可能需要约束一个机载流上的样本频率，使其与另一个机载流的采样频率匹配。 例如，声霸卡与16兼容的适配器可能要求适配器接收器 pin 的采样频率与闩锁在输出 Dac 上时钟的速率一致。

如前文所述，KMixer 是 Windows Server 2003、Windows XP、Windows 2000 和 Windows Me/98 中的系统混音器。 当 KMixer 的源 pin 连接到适配器的接收器 pin 时，KMixer 可能需要调用适配器的 **SetFormat** 方法 (例如，请参阅 [**IMiniportWavePciStream：： SetFormat**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setformat)) ，以调整连接时的采样频率，以匹配输入时音频流的最高采样频率。 如果适配器无法更改频率（也许是因为它受其他板上流的时钟速率的约束），则可能会导致 **SetFormat** 调用失败。 在这种情况下，KMixer 将通过连续降低的采样频率进行更多的 **SetFormat** 调用，直到调用成功。 当 KMixer 以降低的采样频率进行结算后，它将相应地向下采样其更高频率输入流。

 

