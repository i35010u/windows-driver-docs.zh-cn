---
title: 音频的虚拟设备
description: 虚拟的音频设备表示筛选器关系图的呈现和捕获音频内容。 系统音频驱动程序 (SysAudio) 使用可用的硬件和软件组件来确定要生成的筛选器图。
ms.assetid: 0f8ddd2d-f852-4b35-8a18-16416081d3c0
keywords:
- 虚拟音频设备 WDK
- SysAudio
- 系统音频设备 WDK
- 音频虚拟设备 WDK
- 音频筛选器关系图 WDK
- 筛选器关系图中会 WDK 音频、 虚拟音频设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 090b73c229940010c37955529ce65ff3eb1c0aac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526874"
---
# <a name="virtual-audio-devices"></a>音频的虚拟设备


虚拟的音频设备表示筛选器关系图的呈现和捕获音频内容。 系统音频驱动程序 (SysAudio) 使用可用的硬件和软件组件来确定要生成的筛选器图。

有关系统音频驱动程序的详细信息，请参阅[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)。

## <span id="virtual_audio_devices"></span><span id="VIRTUAL_AUDIO_DEVICES"></span>


SysAudio 的客户端包括 DirectSound 并[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)，它可作为 WDM 音频驱动程序特定于音频的 Microsoft Windows 多媒体 Api waveIn、 waveOut、 midiIn、 midiOut、 mixer，之间的接口和aux （Microsoft Windows SDK 文档中所述）。

[KsStudio 实用工具](ksstudio-utility.md)Windows Driver Kit (WDK) 中是绕过 SysAudio 并允许用户手动构造筛选器关系图的应用程序的示例。

以下即插即用设备枚举 SysAudio 以便确定如何构造其客户端可能需要各种音频筛选器关系图将股票的已注册的音频硬件和软件组件。

确定后的筛选器列表关系图，它可以生成的可用的硬件和软件组件，SysAudio 注册为虚拟的音频设备，以播放、 录制、 MIDI 输入/输出、 和混合使用这些关系图。 SysAudio 保留注册表类别 KSCATEGORY\_音频\_专用于其虚拟的音频设备的设备。 适配器驱动程序不应注册本身在此类别中。

SysAudio 客户端可以将视为虚拟的音频设备的筛选器工厂同样到硬件或软件组件的筛选器工厂。 当要求客户端实例化的虚拟设备上特定 pin，SysAudio 自动构造关系图并管理以透明方式与客户端的关系图的内部 pin 连接。 这允许客户端将视为单个筛选器，从而避免复杂的图形管理，例如筛选器间通信问题的筛选器关系图。

 

 




