---
title: 内核模式硬件加速 DDI
description: 内核模式硬件加速 DDI
ms.assetid: f3af3caa-0d1f-4da5-8756-ce71c66d5fb6
keywords:
- DirectMusic 内核模式 WDK 音频
- 内核模式 synths WDK 音频硬件加速
- DirectMusic 内核模式 WDK 音频，有关内核模式
- 内核模式 synths WDK 音频，有关内核模式 synths
- DirectMusic WDK 音频硬件加速
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，内核模式硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4574b9bde77263e94aa93ea7f71e26ed4c961f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333366"
---
# <a name="kernel-mode-hardware-acceleration-ddi"></a>内核模式硬件加速 DDI


## <span id="kernel_mode_hardware_acceleration_ddi"></span><span id="KERNEL_MODE_HARDWARE_ACCELERATION_DDI"></span>


设计指南的此部分包含编写用于启用 DirectMusic 的硬件或软件合成器的内核模式 Dmu 微型端口驱动程序所需的信息。 此处所述的功能是可选的可以实现基本 MIDI 微型端口驱动程序，它支持除了**midiOut**并**midiIn** Api 在 Microsoft Windows 95/98/我，Windows NT 4.0 中，Windows 2000 和更高版本。

实现内核模式组件需要使附件微型端口设备驱动程序接口 (DDI) 允许 WDM MIDI 驱动程序以支持 DirectMusic 硬件加速。 良好的设计策略是首先实现您的驱动程序的用户模式版本并将其转换为内核模式 (请参阅[的用户模式下与内核模式](user-mode-versus-kernel-mode.md))。

如果您不具有执行内核模式下实现之前编写的用户模式版本，请阅读此文档来熟悉的概念，适用于内核模式下的用户模式部分。 在用户模式的示例中引入的常见概念上生成内核模式的讨论。

接下来的两部分提供简要背景的 WDM 内核流式处理以及如何实现用于合成器的微型端口驱动程序的概述：

[DirectMusic WDM 内核流式处理后台](directmusic-wdm-kernel-streaming-background.md)

[合成器微型端口驱动程序概述](synthesizer-miniport-driver-overview.md)

本部分还包括：

[DirectMusic 微型端口驱动程序接口](directmusic-miniport-driver-interface.md)

[语音分配](voice-allocation.md)

[默认的声音样本集](default-sound-sample-sets.md)

[支持的 DirectMusic 属性](support-for-directmusic-properties.md)

 

 




