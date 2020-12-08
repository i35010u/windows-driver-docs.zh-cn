---
title: 虚拟音频设备
description: 虚拟音频设备表示用于呈现和捕获音频内容的筛选器图形。 系统音频驱动程序 (SysAudio) 使用可用的硬件和软件组件来确定要生成的筛选器图。
keywords:
- 虚拟音频设备 WDK
- SysAudio
- 系统音频设备 WDK
- 音频虚拟设备 WDK
- 音频筛选器曲线图 WDK
- 筛选器图形 WDK 音频、虚拟音频设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00fffc08510816c8607aada0e5490335beeadead
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800457"
---
# <a name="virtual-audio-devices"></a>虚拟音频设备


虚拟音频设备表示用于呈现和捕获音频内容的筛选器图形。 系统音频驱动程序 (SysAudio) 使用可用的硬件和软件组件来确定要生成的筛选器图。

有关系统音频驱动程序的详细信息，请参阅 [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)。

## <span id="virtual_audio_devices"></span><span id="VIRTUAL_AUDIO_DEVICES"></span>


SysAudio 的客户端包括 DirectSound 和 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)，它充当 WDM 音频驱动程序与特定于音频的 Microsoft Windows 多媒体 api WaveIn、WaveOut、MidiIn、midiOut、混音器和 aux () Microsoft Windows SDK 文档中所述的接口。

Windows 驱动程序工具包中的 [KsStudio 实用程序](ksstudio-utility.md) (WDK) 是绕过 SysAudio 的应用程序示例，它允许用户手动构造筛选器关系图。

使用 PnP 设备枚举后，SysAudio 将使用已注册的音频硬件和软件组件来确定如何构造其客户端可能需要的各种音频筛选器图。

确定了可从可用硬件和软件组件生成的筛选器图形的列表后，SysAudio 会将这些图形注册为虚拟音频设备以便播放、记录、MIDI 输入/输出和混合。 SysAudio \_ \_ 为其虚拟音频设备保留注册表类别 KSCATEGORY 音频设备。 适配器驱动程序不应在此类别中注册自身。

SysAudio 客户端可以将虚拟音频设备的筛选器工厂视为硬件或软件组件的筛选器工厂。 当客户端需要实例化虚拟设备上的特定 pin 时，SysAudio 会自动构造图形，并以透明方式管理图形的内部 pin 连接到客户端。 这允许客户端将筛选器关系图视为单个筛选器，从而避免了图形管理（例如筛选器之间的通信）的复杂性。

 

 




