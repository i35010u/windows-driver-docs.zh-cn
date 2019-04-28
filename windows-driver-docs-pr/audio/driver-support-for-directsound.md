---
title: 针对 DirectSound 的驱动程序支持
description: 针对 DirectSound 的驱动程序支持
ms.assetid: a32a2a01-4ecd-485f-8293-402a0bcc8336
keywords:
- WDM 音频驱动程序 WDK DirectSound
- 音频驱动程序 WDK DirectSound
- DirectSound WDK 音频
- 有关 DirectSound DirectSound WDK 音频
- 微型端口驱动程序 WDK 音频 DirectSound
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c198d4efb067dfeccfed6519e4a08fd653a5fc1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333745"
---
# <a name="driver-support-for-directsound"></a>针对 DirectSound 的驱动程序支持


## <span id="driver_support_for_directsound"></span><span id="DRIVER_SUPPORT_FOR_DIRECTSOUND"></span>


WDM 音频系统提供的应用程序程序的访问通过 Microsoft DirectSound API 的音频设备驱动程序支持。 提供 DirectSound 驱动程序支持的系统组件的说明，请参阅[WDM 音频组件](wdm-audio-components.md)。

以下部分讨论音频微型端口驱动程序可以实现更好地支持 DirectSound API 向应用程序公开的音频功能的功能。 这些功能包括硬件加速的 2D 和 3D 声音效果，支持各种扬声器配置，并捕获的全双工电话会议的回声等效果。

本部分介绍以下主题：

[DirectSound 硬件加速的 WDM 音频](directsound-hardware-acceleration-in-wdm-audio.md)

[DirectSound 扬声器配置设置](directsound-speaker-configuration-settings.md)

[DirectSound 捕获效果](directsound-capture-effects.md)

 

 




