---
title: 内核模式硬件加速 DDI
description: 内核模式硬件加速 DDI
keywords:
- DirectMusic 内核模式 WDK 音频
- 内核模式 synths WDK 音频，硬件加速
- DirectMusic 内核模式 WDK 音频，关于内核模式
- 内核模式 synths WDK 音频，关于内核模式 synths
- DirectMusic WDK 音频，硬件加速
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频、内核模式硬件加速
- 合成 WDK 音频，内核模式硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b0d2fcdc6388602f05c0d2436259a2c60de38a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784703"
---
# <a name="kernel-mode-hardware-acceleration-ddi"></a>内核模式硬件加速 DDI


## <span id="kernel_mode_hardware_acceleration_ddi"></span><span id="KERNEL_MODE_HARDWARE_ACCELERATION_DDI"></span>


设计指南的此部分包含为启用 DirectMusic 的硬件或软件合成器编写内核模式 Dmu 微型端口驱动程序所需的信息。 此处所述的功能是可选的，并且可以实现基本的 MIDI 微型端口驱动程序，该驱动程序支持 Microsoft Windows 95/98/Me、Windows NT 4.0、Windows 2000 和更高版本下的 **midiOut** 和 **midiIn** api。

实现内核模式组件需要增加微型端口设备驱动程序接口 (DDI) ，以允许 WDM MIDI 驱动程序支持 DirectMusic 硬件加速。 好的设计策略就是首先实现用户模式版本的驱动程序，然后将其转换为内核模式 (查看 [用户模式与内核模式](user-mode-versus-kernel-mode.md)) 。

如果在执行内核模式实现之前尚未编写用户模式版本，请阅读本文档的用户模式部分，以熟悉适用于内核模式的概念。 内核模式讨论基于用户模式示例中引入的常见概念构建。

接下来的两部分提供 WDM 内核流式处理的简短背景，并概述如何为合成器实现微型端口驱动程序：

[DirectMusic WDM 内核流式处理后台](directmusic-wdm-kernel-streaming-background.md)

[合成器微型端口驱动程序概述](synthesizer-miniport-driver-overview.md)

本部分还包括：

[DirectMusic 微型端口驱动程序接口](directmusic-miniport-driver-interface.md)

[语音分配](voice-allocation.md)

[默认的声音样本集](default-sound-sample-sets.md)

[对 DirectMusic 属性的支持](support-for-directmusic-properties.md)

 

 




