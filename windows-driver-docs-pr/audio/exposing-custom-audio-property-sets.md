---
title: 公开自定义音频属性集
description: 公开自定义音频属性集
keywords:
- 硬件加速 WDK DirectSound，自定义音频属性集
- 自定义音频属性集 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cbf9fde0bd755930c350945de7b46911f554e2c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789199"
---
# <a name="exposing-custom-audio-property-sets"></a>公开自定义音频属性集


## <span id="exposing_custom_audio_property_sets"></span><span id="EXPOSING_CUSTOM_AUDIO_PROPERTY_SETS"></span>


DirectSound 支持使用声卡上的自定义属性，并为此目的提供了 **IKsPropertySet** 接口。

**注意**   标头文件 Dsound 和 Ksproxy 定义 **IKsPropertySet** 接口的类似但不兼容版本。 DirectSound 应用程序应使用 Dsound 中定义的版本。 **IKsPropertySet** 的 DirectSound 版本在 Microsoft Windows SDK 文档的 DirectSound 参考页中定义。 有关 KSProxy 版本，请参阅 [IKsPropertySet](/windows-hardware/drivers/ddi/dsound/nn-dsound-ikspropertyset)。

 

默认情况下，在 Windows 98 Second Edition 和 Windows Me 以及 Windows XP 及更高版本中启用自定义音频属性集。 默认情况下，DirectSound 将忽略 Windows 2000 以及 windows Server 2003 和更高版本的 Windows 中的自定义属性集。 为了使 DirectSound 能够识别其中某个操作系统中的自定义属性集，用户必须先在其系统上启用自定义属性集。

例如，若要在 Windows 2000 中启用自定义音频属性集：

1.  在 "控制面板" 中，双击 " **声音和多媒体** " 图标 (或只需 mmsys.cpl) 运行。

2.  在 " **音频** " 选项卡上，在 " **声音播放** " 列表中选择合适的首选设备。

3.  单击“高级”按钮。

4.  在 " **性能** " 选项卡上，将 " **硬件加速** " 滑块滑动到 " **完全**"。

5.  单击“应用” 。

DirectSound 现已启用，可将自定义属性集传递给驱动程序。

" **硬件加速** " 滑块上有四个设置：

-   **无**

-   **基本**

-   **标准**

-   **完整**

仅当滑块设置为 " **完整**" 时，才会启用自定义属性集。 有关详细信息，请参阅 [DirectSound Hardware-Acceleration 和 SRC 滑杆](directsound-hardware-acceleration-and-src-sliders.md)。

 

