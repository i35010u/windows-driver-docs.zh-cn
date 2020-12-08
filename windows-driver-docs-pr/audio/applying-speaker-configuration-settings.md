---
title: 应用 Speaker-Configuration 设置
description: 应用 Speaker-Configuration 设置
keywords:
- 扬声器失败-配置请求 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2d9953b54f1cf95f4a6f5742a84e1004c8d97fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785029"
---
# <a name="applying-speaker-configuration-settings"></a>应用 Speaker-Configuration 设置


## <span id="applying_speaker_configuration_settings"></span><span id="APPLYING_SPEAKER_CONFIGURATION_SETTINGS"></span>


**注意**  此信息适用于 Windows XP 及更早版本的操作系统。 从 Windows Vista 开始， **IDirectSound：： GetSpeakerConfig** 和 **IDirectSound：： SetSpeakerConfig** 已弃用。

 

DirectSound 将跟踪其当前的扬声器配置设置，并在每次创建新的 DirectSound 设备时将该设置应用于音频硬件。

应用程序可以通过调用 **IDirectSound：： SetSpeakerConfig** 方法来更改系统范围的扬声器配置，该方法更新注册表中的扬声器配置设置。 方法还尝试对硬件立即应用新设置，尽管音频设备通常无法在 DirectSound 对象存在时更改扬声器设置。 有关 DirectSound 为此方法定义的扬声器配置的列表，请参阅 [转换 Speaker-Configuration 请求](translating-speaker-configuration-requests.md)。

用户可以通过 " **媒体属性** " 页中的 "扬声器配置" 对话框（在 "控制面板" 中 ( # A0) 来更改配置。 例如，若要查找 Windows XP 下的 DirectSound 扬声器配置对话框，请遵循以下步骤：

1.  在 "控制面板" 中，双击 " **声音和音频设备** " 图标。

2.  在 " **音频** " 选项卡上，从 " **声音播放** " 列表中选择一个设备。

3.  选择“高级”按钮。

4.  选择 " **扬声器** " 选项卡。

此时，你应该会看到 "扬声器设置" 旁边的标签 **设置** ，你可以从中进行选择。

DirectSound 使用 [**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](./ksproperty-audio-channel-config.md) 设置属性请求将演讲者配置信息发送到3d 节点或 DAC 节点 (在音频筛选器关系图中) [**KSNODETYPE \_ 3d \_ 效果**](./ksnodetype-3d-effects.md) 或 [**KSNODETYPE \_ DAC**](./ksnodetype-dac.md) 。 对于3D 节点，属性请求的目标实际上是 (3D 流对象) 的固定节点。 对于 DAC 节点，目标是包含 DAC 节点的筛选器对象。 无论是哪种情况，演讲者配置设置都是全局性的，并影响音频设备整体。 随后运行的所有音频应用程序都将受新设置的限制，直到 DirectSound 再次更改设置。

请注意，只有 Windows Me 附带的 DirectSound 版本以及 Windows XP 及更高版本，将发言人配置属性请求发送到 DAC 节点-DirectSound 的早期版本不支持此功能。 但是，所有版本的 DirectSound 将这些请求发送到3D 节点。

如果应用程序已创建多个3D 节点，则 DirectSound 仅向要创建的第一个3D 节点发送发言人配置请求。

每次应用程序创建 DirectSound 对象或调用 **IDirectSound：： SetSpeakerConfig** 方法时，DirectSound 都会将演讲者配置请求发送到3D 和 DAC 节点。 音频设备在管理活动流时，通常无法更改其扬声器配置，DirectSound 尝试尽可能避免此限制。 例如，在创建 DirectSound 对象时，DirectSound 会在实例化筛选器后、在筛选器中实例化任何 pin 之前发送发言人配置请求，即在创建任何流之前。

如果调用 **SetSpeakerConfig**，则此限制更难避免。 当应用程序调用 **SetSpeakerConfig** 时，适配器驱动程序通常无法 DirectSound 的发言人配置请求。 这是因为 DirectSound 对象已存在，这意味着该设备已经具有要管理的活动流。

在这种情况下，适配器驱动程序有两个选项可用于处理扬声器配置请求失败：

-   驱动程序可以记住请求的配置，并在其所有流销毁后立即应用。

-   驱动程序可以忽略请求，并依赖 DirectSound 在下次创建 DirectSound 对象时发送另一个发言人配置请求。

第一种方法可提供更好的用户体验，因为如果用户通过 "扬声器配置" 对话框选择了新设置，则更改会立即在所有应用程序中生效-而不只是 DirectSound 应用程序。 当然，如果在选择新设置时运行任何音频应用程序，更改将推迟到所有音频应用程序终止之前。 ) 使用第二个选项，但是，在 DirectSound 应用程序运行之前，更改不会生效。 ( 例如，如果使用 Windows 多媒体 waveOut API 的应用程序是在更改控制面板设置后运行的第一个应用程序，则用户可能会想知道新设置没有明显的效果。

为了响应发送到3D 或 DAC 节点的发言人配置请求，典型的适配器驱动程序仅在任何音频应用程序当前未实例化任何 pin 时才更新音频硬件中的扬声器配置。 这意味着，如果 waveOut 应用程序（例如）在第二个应用程序调用 **DirectSoundCreate** 时打开一个或多个 pin，驱动程序可能需要将对音频设备扬声器配置的任何挂起的更改推迟到以后的时间。

如果你的驱动程序无法完成更改设备扬声器配置的请求，则该请求应仅失败。 在 DirectSound 对象创建或 **SetSpeakerConfig** 调用期间，如果无法进行发言人配置请求，则不会导致 DirectSound 对象创建或 **SetSpeakerConfig** 调用失败。

在启动时，音频适配器驱动程序会将硬件的扬声器配置初始化为其默认设置，通常为立体声。 一旦任何应用程序创建 DirectSound 对象，DirectSound 就会将注册表中存储的设置应用到硬件。 应用程序必须先创建 DirectSound 设备，然后才能调用 **SetSpeakerConfig** 来更改注册表中的扬声器配置设置，但此注册表设置通常仅在 DirectSound 设备发布后才会在硬件中生效，并会创建第二个 DirectSound 设备。

安装音频设备后、扬声器配置出错时，DirectSound 扬声器配置会立即默认为立体声。

 

