---
title: 专有的 Speaker-Configuration 实用程序
description: 专有的 Speaker-Configuration 实用程序
keywords:
- 专用发言人-配置实用工具 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f29f1c2babecefb32224b7ea764b187cea9b0480
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800777"
---
# <a name="proprietary-speaker-configuration-utilities"></a>专有的 Speaker-Configuration 实用程序


## <span id="proprietary_speaker_configuration_utilities"></span><span id="PROPRIETARY_SPEAKER_CONFIGURATION_UTILITIES"></span>


**注意**  此信息适用于 Windows XP 及更早版本的操作系统。 从 Windows Vista 开始， **IDirectSound：： GetSpeakerConfig** 和 **IDirectSound：： SetSpeakerConfig** 已弃用。

 

硬件供应商有时会提供要与音频驱动程序一起使用的专用发言人配置实用程序，以代替控制面板中的 "扬声器" 对话框。 此类实用工具有一个潜在的问题：有时以无法通知 Windows 的专有方式更改扬声器配置。 如果专有实用工具中的设置与 "控制面板" 中的设置不匹配，这可能会导致用户体验不佳。 如果你认为你的设备需要专用实用程序，则应执行以下步骤，将你的实用工具与 Windows 集成：

1.  在支持 [**KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG**](./ksproperty-audio-channel-config.md) 属性的驱动程序中实现 DAC 节点。 通过此节点，Windows 会向驱动程序通知用户在 "控制面板" 中所做的更改。

2.  通过调用 DirectSound 方法 **GetSpeakerConfig** 和 **SetSpeakerConfig** 设计配置实用工具来管理扬声器配置。

**SetSpeakerConfig** 调用通知 DirectSound (和 Windows) 你的实用工具对扬声器配置所做的更改。 此外，实用工具的初始化代码应调用 **GetSpeakerConfig** 来确定用户是否已通过控制面板更改了任何设置。 如果是这样，则实用程序应在其用户界面中反映这些更改。

如果你的设备支持没有精确的 Windows 等效项的多通道格式，则配置实用工具应执行以下操作：

-   当更改为没有精确 Windows 等效项的扬声器配置时，请使用最接近的 Windows 等效项调用 **SetSpeakerConfig** 。 这是对配置驱动程序所需的任何专有调用的补充。

-   更改为具有精确的 Windows 等效项的发言人配置时，请调用 **SetSpeakerConfig** 来更新扬声器模式。

如果使 Windows 更容易识别设备的功能，则 DirectSound 可以启用某些功能，否则无法启用 (例如，多通道3D 平移) 。

 

