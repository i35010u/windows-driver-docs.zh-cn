---
title: 公开自定义音频属性集
description: 公开自定义音频属性集
ms.assetid: dc45f0fb-f462-4d20-967a-0665e18019e4
keywords:
- 硬件加速 WDK DirectSound，自定义音频属性设置
- 自定义音频属性集 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9222b10691459a31fd286f8fe9a5ca7246750dd2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360077"
---
# <a name="exposing-custom-audio-property-sets"></a>公开自定义音频属性集


## <span id="exposing_custom_audio_property_sets"></span><span id="EXPOSING_CUSTOM_AUDIO_PROPERTY_SETS"></span>


DirectSound 声卡上支持自定义属性的用法，并提供**IKsPropertySet**接口实现此目的。

**请注意**   Dsound.h 和 Ksproxy.h 标头文件定义的类似，但并不兼容版本**IKsPropertySet**接口。 DirectSound 应用程序应使用 Dsound.h 中定义的版本。 DirectSound 新版**IKsPropertySet** DirectSound 参考页中的 Microsoft Windows SDK 文档中定义。 有关 KSProxy 版本，请参阅[IKsPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dsound/nn-dsound-ikspropertyset)。

 

自定义音频属性集是已启用默认情况下，在 Windows 98 Second Edition 和 Windows Me，并在 Windows XP 及更高版本。 默认情况下，DirectSound 将忽略在 Windows 2000 和 Windows Server 2003 和更高版本的服务器版本的 Windows 中的自定义属性集。 为识别的自定义属性设置在这些操作系统之一的 DirectSound，用户必须先启用其系统上的自定义属性集。

例如，若要启用自定义音频属性设置在 Windows 2000 中：

1.  在控制面板中，双击**声音和多媒体**图标 （或只需运行的 mmsys.cpl）。

2.  上**音频**选项卡上，选择在相应的首选的设备**声音播放**列表。

3.  单击“高级”  按钮。

4.  上**性能**选项卡上，滑动**硬件加速**滑块移至**完整**。

5.  单击 **“应用”** 。

DirectSound 现在能够将自定义属性集传递给驱动程序。

四个设置位于**硬件加速**滑块：

-   **无**

-   **基本**

-   **标准**

-   **Full**

启用自定义属性集时，仅在滑块设置为**完整**。 有关详细信息，请参阅[DirectSound 硬件加速和 SRC 滑块](directsound-hardware-acceleration-and-src-sliders.md)。

 

 




