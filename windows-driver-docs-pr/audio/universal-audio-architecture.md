---
title: 通用音频体系结构
description: Microsoft 通用音频体系结构 (UAA) 启用符合体系结构，以完全依赖于驱动程序支持的操作系统的音频设备。
ms.assetid: a42eff33-7952-4004-903d-9b202d1864b9
keywords:
- UAA WDK
- 通用音频体系结构 WDK
- 音频设备 WDK UAA
- PCI 音频适配器 WDK
- USB WDK 音频
- IEEE 1394 WDK 音频
- Intel 高清晰度音频规范
- WDM 音频驱动程序 WDK，通用音频体系结构
- 音频驱动程序 WDK，通用音频体系结构
- 1394 WDK 音频
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18ac085175fe4928f6772e27b094f0f4e08927b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521820"
---
# <a name="universal-audio-architecture"></a>通用音频体系结构


Microsoft 通用音频体系结构 (UAA) 启用符合体系结构，以完全依赖于驱动程序支持的操作系统的音频设备。

若要 UAA 兼容，PCI 音频适配器必须符合是 Intel 音频编解码器 97 (AC'97) 规范的后续版本的 Intel 高清晰度音频规范。 与不同 AC'97，Intel 高清晰度音频 (Intel HD Audio) 标准化的总线控制器，除了编解码器的设备和串行接口链接 （连接到编解码器的控制器的链接）。 Intel HD 音频设备的 UAA 设计指南包含不是 Intel 高清晰度音频规范的一部分的其他要求。 Windows Vista 为 UAA 符合 PCI 音频适配器提供完整的驱动程序支持。

若要 UAA 兼容，USB 音频设备必须符合对 USB 音频规范和 USB 音频设备 UAA 设计指南。 USB 音频设备可以进行利用[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)(Usbaudio.sys)，这作为 Windows 的一部分提供。 根据定义，与 Windows 中的 USBAudio 类系统驱动程序兼容的 USB 音频设备与 UAA 兼容。

若要 UAA 兼容，IEEE 1394 AV/C 音频设备必须符合相关的 IEEE 1394 规范和 IEEE 1394 AV/C 音频设备 UAA 设计指南。 使用 IEEE 1394 音频设备可以进行[AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)(Avcaudio.sys)，这作为 Windows 的一部分提供。

有关 Microsoft UAA 计划的详细信息，请参阅[通用音频体系结构](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/UAA_Guidelines.doc)白皮书。 有关 Intel HD Audio 的详细信息，请参阅[Intel HD Audio](https://go.microsoft.com/fwlink/p/?linkid=42508)网站。 USB 和 IEEE 1394 音频设备的相关规范的列表，请参阅[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)并[AVCAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)。

 

 




