---
title: 音频的适配器的其他安装问题
description: 音频的适配器的其他安装问题
ms.assetid: fcfa9c41-7fad-4b22-9054-a1debb972580
keywords:
- 音频适配器 WDK，安装
- 适配器驱动程序 WDK 音频，安装
- 端口类音频适配器 WDK，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc213ade503bb193ad906a3414e5104d33a0c7f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532940"
---
# <a name="miscellaneous-installation-issues-for-an-audio-adapter"></a>音频的适配器的其他安装问题


## <span id="miscellaneous_installation_issues_for_an_audio_adapter"></span><span id="MISCELLANEOUS_INSTALLATION_ISSUES_FOR_AN_AUDIO_ADAPTER"></span>


列出了最常见的安装问题的音频的适配器：

-   初始安装期间的音频设备或进行会破坏现有的音频设置的操作系统升级时，应确保该驱动程序，设置将初始化为合理的默认值。 有关详细信息，请参阅[默认音频音量设置](default-audio-volume-settings.md)。

-   有时在安装期间，OEM 想要重写默认音频音量级别或进行硬编码音频类驱动程序的默认麦克风提升级别。 这是不可能高达 Windows 7 的 Windows 的早期版本中实现的。 在 Windows 8 和更高版本，现在可以自定义这些设置的默认值。 有关如何执行此操作的详细信息，请参阅[自定义默认音频音量设置](customizing-default-audio-volume-settings.md)。

-   在 Windows Vista 和更高版本操作系统中，将音频设备的主音量级别的默认设置是六个分贝的衰减，并在安装时设置。 无论何种频率重新启动您的计算机将保留此默认主音量级别设置或安装完成后，选择的任何其他级别。 若要选择退出卷级持久性可用于 AddProperty 注册表指令的 INF 文件，请通过设置主键的值\_AudioDevice\_DontPersistControls 注册表项。 有关如何执行此操作的详细信息，请参阅[选择的卷级别持久性](opting-out-of-volume-level-persistence.md)。

-   进行操作系统升级时，可以经常保留音频设备的已安装的驱动程序和注册表设置。 有关如何使此过程对用户透明的指南，请参阅[操作系统升级](operating-system-upgrades.md)。

-   音频驱动程序轻松地设计为允许多个音频适配器卡插入到同一系统的相同实例。 有关详细信息，请参阅[系统范围内唯一设备 Id](system-wide-unique-device-ids.md)。

-   INF 文件关键字所共有的所有设备类的列表，请参阅[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。 但是，此列表不包含多个特定于媒体的关键字。 有关详细信息，请参阅[特定于媒体的 INF 文件关键字](media-specific-inf-file-keywords.md)。

-   有关如何适配器驱动程序或微型端口驱动程序可以获取安装信息从注册表的信息，请参阅[检索设备安装程序信息](retrieving-device-setup-information.md)。

-   有关 Windows Vista 所支持的音频适配器不具有物理卷控件旋钮的信息，请参阅[Windows Vista 软件卷控件支持](https://msdn.microsoft.com/library/windows/hardware/ff539263)主题。

 

 




