---
title: 采样频率的硬件约束
description: 采样频率的硬件约束
ms.assetid: e0041fd9-073c-4779-a3cf-6d0527ba847b
keywords:
- 采样频率约束 WDK 音频
- 约束采样频率 WDK 音频
- 硬件约束 WDK 音频
- 频率约束 WDK 音频
- 数据交集处理程序 WDK 音频，示例频率约束
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45e6c7916fb3d4332454f252462cf68d2e713e3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533192"
---
# <a name="hardware-constraints-on-sample-frequency"></a>采样频率的硬件约束


## <span id="hardware_constraints_on_sample_frequency"></span><span id="HARDWARE_CONSTRAINTS_ON_SAMPLE_FREQUENCY"></span>


一些音频设备要求的示例适配器筛选器的接收器 pin 频率匹配数字的输出端口或来自麦克风的输入的流的频率。 例如，声音 Blaster 16 兼容硬件通常具有单个 crystal，这样可约束其输入和输出流，若要在相同的时钟速率运行。 可以为其各种板载音频流中支持多个时钟速度的适配器仍可能需要不同时钟速率数限制为一些小的数字。

出于这些原因，适配器驱动程序可能需要限制上一个载入流以匹配的另一个载入流采样频率。 例如，声音 Blaster 16 兼容适配器可能要求的示例适配器的接收器 pin 频率匹配的闩锁工作在输出的速率 Dac。

正如上文 KMixer 我是在 Windows Server 2003、 Windows XP、 Windows 2000 和 Windows 系统 mixer / 98。 KMixer 当 KMixer 的源 pin 连接到适配器的接收器 pin 时，可能需要调用该适配器**SetFormat**方法 (有关示例，请参阅[ **IMiniportWavePciStream::SetFormat** ](https://msdn.microsoft.com/library/windows/hardware/ff536732))若要调整示例频率，在要在其输入音频流的最高示例频率相匹配的连接。 如果适配器不能更改的频率-可能是因为受限制的其他开发板的流-的时钟速率，它可能会失败**SetFormat**调用。 在这种情况下，通过使多个响应 KMixer **SetFormat**具有连续低示例频率直到调用成功的调用。 一旦 KMixer 已经开始在降低采样频率，它将示例取其较高的频率输入的流相应地。

 

 




