---
title: 呈现和捕获音频使用端口类音频适配器
description: 呈现和捕获音频使用端口类音频适配器
ms.assetid: a6f47f94-eaff-47bf-b9e5-fc6d4b8d25fd
keywords:
- 端口类适配器驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 645dd01cbe0ffd19fbce5d22d60a2f4bb2df89bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328723"
---
# <a name="rendering-and-capturing-audio-content-by-using-a-port-class-audio-adapter"></a>使用端口类音频适配器呈现和捕获音频内容


## <span id="ddk_rendering_and_capturing_audio_content_by_using_a_port_class_audio_"></span><span id="DDK_RENDERING_AND_CAPTURING_AUDIO_CONTENT_BY_USING_A_PORT_CLASS_AUDIO_"></span>


下图显示了端口类音频适配器驱动程序的呈现和捕获音频内容的配置。

![说明呈现，使用端口类音频适配器驱动程序捕获音频内容的关系图](images/portcls.png)

查看有关 Microsoft Windows 驱动程序模型 (WDM) 音频组件的说明以下信息：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[DirectMusic 系统组件](user-mode-wdm-audio-components.md#directmusic_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[拆分器系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

请参阅以下有关批、 MIDI、 DirectMusic 和拓扑的筛选器信息：

[批筛选器](wave-filters.md)

[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md)

[拓扑筛选器](topology-filters.md)

请参阅以下有关位于端口类音频适配器上方的筛选器图形的详细信息：

[呈现和捕获批内容](rendering-and-capturing-wave-content.md)

[呈现和捕获 MIDI 内容](rendering-and-capturing-midi-content.md)

 

 




