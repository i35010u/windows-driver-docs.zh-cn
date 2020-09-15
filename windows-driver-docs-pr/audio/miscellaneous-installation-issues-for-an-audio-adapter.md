---
title: 音频适配器的其他安装问题
description: 音频适配器的其他安装问题
ms.assetid: fcfa9c41-7fad-4b22-9054-a1debb972580
keywords:
- 音频适配器 WDK，安装
- 适配器驱动程序 WDK 音频，安装
- 端口类音频适配器 WDK，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b433b53df0e47fabf39738cf04ef9c6ea2ec1f1
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102308"
---
# <a name="miscellaneous-installation-issues-for-an-audio-adapter"></a>音频适配器的其他安装问题


## <span id="miscellaneous_installation_issues_for_an_audio_adapter"></span><span id="MISCELLANEOUS_INSTALLATION_ISSUES_FOR_AN_AUDIO_ADAPTER"></span>


列出的音频适配器最常见的安装问题如下：

-   在音频设备的初始安装过程中，或在对现有音频设置进行操作系统升级时，驱动程序应确保将设置初始化为合理的默认值。 有关详细信息，请参阅 [默认音频音量设置](default-audio-volume-settings.md)。

-   有时，在安装过程中，OEM 希望覆盖默认音频音量级别，或由音频类驱动程序硬编码的默认麦克风提升级别。 在 windows 的早期版本中不可能出现这种情况。 在 Windows 8 及更高版本中，现在可以自定义这些设置的默认值。 有关如何执行此操作的详细信息，请参阅 [自定义默认音频音量设置](customizing-default-audio-volume-settings.md)。

-   在 Windows Vista 和更高版本的操作系统中，音频设备的主音量级别的默认设置为6分贝的衰减，在安装时设置该设置。 此默认的主音量级别设置或安装后选择的任何其他级别，不管你重新启动计算机的频率如何，都不会保留。 若要选择退出卷级持久性，可以通过 INF 文件使用 AddProperty 注册表指令来设置 PKEY \_ AudioDevice \_ DontPersistControls 注册表项的值。 有关如何执行此操作的详细信息，请参阅退出 [卷级持久性](opting-out-of-volume-level-persistence.md)。

-   在操作系统升级过程中，可以经常保留音频设备的已安装驱动程序和注册表设置。 有关如何使此过程对用户透明的指导，请参阅 [操作系统升级](operating-system-upgrades.md)。

-   音频驱动程序可以轻松地设计为允许将多个相同的音频适配器实例插入同一系统。 有关详细信息，请参阅 [系统范围的唯一设备 id](system-wide-unique-device-ids.md)。

-   有关所有设备类共有的 INF 文件关键字的列表，请参阅 [Inf 文件部分和指令](../install/index.md)。 但是，此列表不包含多个特定于媒体的关键字。 有关详细信息，请参阅 [特定于媒体的 INF 文件关键字](media-specific-inf-file-keywords.md)。

-   有关适配器驱动程序或微型端口驱动程序如何从注册表获取安装信息的信息，请参阅 [检索设备安装信息](retrieving-device-setup-information.md)。

-   有关 Windows Vista 对不具有物理音量控制旋钮的音频适配器的支持的信息，请参阅 [Windows Vista 软件音量控制支持](./software-volume-control-support.md) 主题。

