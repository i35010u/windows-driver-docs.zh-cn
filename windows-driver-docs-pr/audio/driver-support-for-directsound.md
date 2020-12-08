---
title: 针对 DirectSound 的驱动程序支持
description: 针对 DirectSound 的驱动程序支持
keywords:
- WDM 音频驱动程序 WDK，DirectSound
- 音频驱动程序 WDK，DirectSound
- DirectSound WDK 音频
- DirectSound WDK 音频，关于 DirectSound
- 微型端口驱动程序 WDK 音频，DirectSound
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c7225f94d0d77a5341548ba1b560a1b0a9cf2b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786571"
---
# <a name="driver-support-for-directsound"></a>针对 DirectSound 的驱动程序支持


## <span id="driver_support_for_directsound"></span><span id="DRIVER_SUPPORT_FOR_DIRECTSOUND"></span>


WDM 音频系统为通过 Microsoft DirectSound API 访问音频设备的应用程序提供驱动程序支持。 有关提供 DirectSound 驱动程序支持的系统组件的说明，请参阅 [WDM 音频组件](wdm-audio-components.md)。

以下部分讨论音频微型端口驱动程序可实现的功能，以更好地支持 DirectSound API 向应用程序公开的音频功能。 这些功能包括：二维和三维声音效果的硬件加速、支持各种扬声器配置和捕获效果，如全双工电话会议的回声抵消。

本部分介绍以下主题：

[WDM 音频中的 DirectSound 硬件加速](directsound-hardware-acceleration-in-wdm-audio.md)

[DirectSound Speaker-Configuration 设置](directsound-speaker-configuration-settings.md)

[DirectSound 捕获效果](directsound-capture-effects.md)

 

 




