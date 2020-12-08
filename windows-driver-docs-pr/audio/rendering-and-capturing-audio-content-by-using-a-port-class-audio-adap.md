---
title: 使用端口类音频适配器呈现和捕获音频
description: 使用端口类音频适配器呈现和捕获音频
keywords:
- 端口类适配器驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 883f8b7a25487a673b0cb3facf3cd650f61fd472
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800737"
---
# <a name="rendering-and-capturing-audio-content-by-using-a-port-class-audio-adapter"></a>使用端口类音频适配器呈现和捕获音频内容


## <span id="ddk_rendering_and_capturing_audio_content_by_using_a_port_class_audio_"></span><span id="DDK_RENDERING_AND_CAPTURING_AUDIO_CONTENT_BY_USING_A_PORT_CLASS_AUDIO_"></span>


下图显示了用于呈现和捕获音频内容的端口类音频适配器驱动程序的配置。

![说明如何使用端口类音频适配器驱动程序呈现和捕获音频内容的示意图](images/portcls.png)

请参阅以下内容，了解 Microsoft Windows 驱动模型 (WDM) 音频组件：

[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)

[DirectMusic 系统组件](user-mode-wdm-audio-components.md#directmusic_system_component)

[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul 系统驱动程序](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[拆分系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

请参阅以下内容，了解有关 wave、MIDI、DirectMusic 和拓扑筛选器的信息：

[滤波器](wave-filters.md)

[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md)

[拓扑筛选器](topology-filters.md)

请参阅以下内容，了解有关位于端口类音频适配器上方的筛选器关系图的详细信息：

[呈现和捕获 Wave 内容](rendering-and-capturing-wave-content.md)

[呈现和捕获 MIDI 内容](rendering-and-capturing-midi-content.md)

 

 




