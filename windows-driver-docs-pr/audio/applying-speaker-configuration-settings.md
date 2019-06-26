---
title: 应用 Speaker-Configuration 设置
description: 应用 Speaker-Configuration 设置
ms.assetid: 98fe96cc-8436-4400-9b39-86d188e085c9
keywords:
- 失败的扬声器配置请求 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d784b07b048aeb3e56329831de24d9922f1ceaf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355757"
---
# <a name="applying-speaker-configuration-settings"></a>应用 Speaker-Configuration 设置


## <span id="applying_speaker_configuration_settings"></span><span id="APPLYING_SPEAKER_CONFIGURATION_SETTINGS"></span>


**请注意**  此信息适用于 Windows XP 和早期版本的操作系统。 从 Windows Vista 开始**IDirectSound::GetSpeakerConfig**并**IDirectSound::SetSpeakerConfig**已弃用。

 

DirectSound 跟踪其当前的扬声器配置设置在注册表中，并适用，将设置为的音频硬件每次设备创建新 DirectSound。

应用程序可以通过调用更改系统范围内扬声器配置**IDirectSound::SetSpeakerConfig**方法，更新注册表中的扬声器配置设置。 此方法还尝试将应用新的设置立即硬件，尽管音频设备通常无法 DirectSound 对象存在时更改扬声器的设置。 DirectSound 定义此方法的演讲者配置的列表，请参阅[翻译扬声器配置请求](translating-speaker-configuration-requests.md)。

用户可以更改通过中的扬声器配置对话框配置**多媒体属性**控制面板中的页 (mmsys.cpl)。 若要查找 Windows XP 下的 DirectSound 扬声器配置对话框中，例如，请执行以下步骤：

1.  在控制面板中，双击**声音和音频设备**图标。

2.  上**音频**选项卡上，选择从一个设备**声音播放**列表。

3.  单击“高级”  按钮。

4.  单击**扬声器**选项卡。

此时，应看到的标签**扬声器设置**旁边扬声器配置，可以从中进行选择的列表。

使用 DirectSound [ **KSPROPERTY\_音频\_通道\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)集属性请求将扬声器配置信息发送给三维节点或 DAC节点 ([**KSNODETYPE\_3D\_效果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)或者[ **KSNODETYPE\_DAC** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)) 音频筛选器关系图中。 对于三维节点，属性请求的目标是实际的 pin （3D 流对象），源节点。 有关 DAC 的节点中，目标是包含 DAC 节点的筛选器对象。 在任一情况下，扬声器配置设置是全局的并且影响作为一个整体的音频设备。 随后运行的所有音频应用程序可能会有所新的设置，直到 DirectSound 更改该设置再次。

请注意，DirectSound 的唯一版本随 Windows Me，和 Windows XP 和更高版本，扬声器配置属性将请求发送到 DAC 节点--DirectSound 的早期版本不支持此功能。 但是，所有版本的 DirectSound 将这些请求都发送到三维的节点。

如果应用程序创建了多个三维节点，DirectSound 仅对要创建的第一个 3D 节点发送扬声器配置请求。

DirectSound 将扬声器配置请求发送到 3D 和 DAC 节点每次应用程序创建 DirectSound 对象或调用**IDirectSound::SetSpeakerConfig**方法。 音频设备是通常无法更改其扬声器配置，而他们管理活动流和 DirectSound 尝试避免此限制，在可能的情况。 例如，创建 DirectSound 对象时，DirectSound 发送扬声器配置请求实例化筛选器之后但在实例上的筛选器-也就是说，任何 pin 之前创建的所有流化之前。

此限制，避免在调用的情况下更加困难**SetSpeakerConfig**。 当应用程序调用**SetSpeakerConfig**，适配器驱动程序通常会失败，DirectSound 的扬声器配置请求。 这是因为 DirectSound 对象已存在，这意味着该设备已有活动流来管理。

在这种情况下，适配器驱动程序具有用于处理已失败的扬声器配置请求的两个选项：

-   该驱动程序可以记住所请求的配置，并将其应用只是立即销毁所有流。

-   该驱动程序可以忽略该请求，并且依赖于 DirectSound 发送另一个扬声器配置请求创建一个 DirectSound 对象的下一个时间。

第一个选项可以提供更好的用户体验，因为如果用户选择新的设置通过扬声器配置对话框，更改将立即生效中所有应用程序-不只是 DirectSound 应用程序。 （当然，如果音频的任何应用程序运行在选择新设置时，此更改会推迟到音频的所有应用程序终止。）使用第二个选项，但是，更改才会生效 DirectSound 应用程序运行之前。 例如，如果使用 Windows 多媒体 waveOut API 的应用程序是第一个应用程序中，若要更改控件面板设置后运行，用户可能想知道为什么新设置不起作用很明显。

发送到 3D 或 DAC 节点的扬声器配置请求响应，典型的适配器驱动程序更新的音频硬件中的扬声器配置，仅当没有 pin 当前通过任何音频的应用程序实例化。 这意味着，如果一个 waveOut 应用程序，例如，有一个或多个插针打开第二个应用程序调用时**DirectSoundCreate**，驱动程序可能需要延迟对音频设备的演讲者任何挂起的更改到更高版本时的配置。

如果您的驱动程序无法满足请求以更改设备的扬声器配置，它只是应失败请求。 DirectSound 对象创建过程失败的扬声器配置请求或**SetSpeakerConfig**调用不会导致 DirectSound 对象创建或**SetSpeakerConfig**调用失败。

在启动时，音频适配器驱动程序初始化为默认设置，这是通常立体声的硬件的扬声器配置。 只要任何应用程序创建 DirectSound 对象时，DirectSound 应用到的硬件在注册表中存储的设置。 应用程序必须创建 DirectSound 设备，然后才能调用**SetSpeakerConfig**若要更改注册表中，但此注册表中的扬声器配置设置通常设置的硬件中之后才生效DirectSound 设备发布并创建第二个 DirectSound 设备。

在安装的音频设备或扬声器配置错误发生时后立即, DirectSound 演讲者配置为立体声的默认值。

 

 




