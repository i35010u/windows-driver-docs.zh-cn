---
title: 专有扬声器配置实用程序
description: 专有扬声器配置实用程序
ms.assetid: d04b8c1b-13c6-422f-b13a-909f7074ac75
keywords:
- 专有扬声器配置实用程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5836daea553c951b31be90b572ce59b19c660d0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523573"
---
# <a name="proprietary-speaker-configuration-utilities"></a>专有扬声器配置实用程序


## <span id="proprietary_speaker_configuration_utilities"></span><span id="PROPRIETARY_SPEAKER_CONFIGURATION_UTILITIES"></span>


**请注意**  此信息适用于 Windows XP 和早期版本的操作系统。 从 Windows Vista 开始**IDirectSound::GetSpeakerConfig**并**IDirectSound::SetSpeakerConfig**已弃用。

 

硬件供应商偶尔提供专用的扬声器配置实用程序用于替代在控制面板的演讲者对话框其音频驱动程序。 此类实用程序有潜在问题： 他们有时无法通知更改的 Windows 的专有方式更改扬声器配置。 如果在专有实用程序中的设置不匹配那些在控制面板中，这可能导致不良用户体验。 如果你认为你的设备需要一个专用的实用程序，应采取以下步骤以将与 Windows 集成实用程序：

1.  在您支持的驱动程序中实现 DAC 节点[ **KSPROPERTY\_音频\_通道\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537250)属性。 通过此节点中，Windows 会通知立即通过控制面板中的用户所做的更改的驱动程序。

2.  设计配置实用程序，以通过调用 DirectSound 方法来管理扬声器配置**GetSpeakerConfig**并**SetSpeakerConfig**。

**SetSpeakerConfig**调用通知实用程序对做的更改扬声器配置 DirectSound （和 Windows）。 此外，应调用实用程序的初始化代码**GetSpeakerConfig**来确定用户是否已更改通过控制面板的任何设置。 如果是这样，该实用程序应反映这些更改在其用户界面中。

如果你的设备支持多渠道具有不精确的 Windows 等效项的格式，配置实用程序应执行以下操作：

-   更改为没有精确 Windows 等效项的演讲者配置时，调用**SetSpeakerConfig**与最接近 Windows 等效项。 这是进行任何专有调用所需配置的驱动程序的补充。

-   更改为具有精确 Windows 等效项的演讲者配置时，调用**SetSpeakerConfig**若要更新的演讲者模式。

如果使 Windows 设备的功能的更好地识别，DirectSound 可以启用它无法否则启用某些功能 （例如，多渠道三维平移）。

 

 




