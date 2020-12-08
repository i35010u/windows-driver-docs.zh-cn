---
title: 操作系统升级
description: 操作系统升级
keywords:
- 音频适配器 WDK，操作系统升级
- 适配器驱动程序 WDK 音频，操作系统升级
- 端口类音频适配器 WDK，操作系统升级
- 保留音频设置 WDK 音频
- 迁移 DLL WDK 音频
- 迁移设置 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28fbac33ab98736817c99fbf1a0bacaa4b545571
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800973"
---
# <a name="operating-system-upgrades"></a>操作系统升级


## <span id="operating_system_upgrades"></span><span id="OPERATING_SYSTEM_UPGRADES"></span>


音频设备的驱动程序和注册表设置可以经常在操作系统升级时保留。 以下讨论介绍了实现这一点的一些准则。

### <a name="span-idpreserving_audio_settingsspanspan-idpreserving_audio_settingsspanspan-idpreserving_audio_settingsspanpreserving-audio-settings"></a><span id="Preserving_Audio_Settings"></span><span id="preserving_audio_settings"></span><span id="PRESERVING_AUDIO_SETTINGS"></span>保留音频设置

音频适配器驱动程序可以在系统注册表中跟踪其当前设备设置--主要卷级别和静音设置。 驱动程序通常将这些设置存储在系统提供的驱动程序密钥中， (在 "设置" 子项下由 INF 关键字 HKR) 表示。 当用户通过控制面板或其他音频应用程序更改这些设置时，驱动程序将更新相应的注册表项。 系统每次启动时，驱动程序都会从注册表还原设备设置。

从 Windows Me/98 升级到 Windows XP 或 Windows 2000 时，Windows 安装程序无法保留这些设置。

但是，从 Windows 98 升级到 Windows Me 或从一个基于 NT 的操作系统升级到另一个 (例如，从 Windows 2000 升级到 Windows XP) 时，安装程序会将驱动程序的现有注册表设置保持不变。 用户很大程度上喜欢此行为，因为它保留了在一段时间内对系统进行的调整，而不是强制他们尝试在每次升级操作系统时手动还原其设置。

但是，某些专有驱动程序在每次安装时都会用默认值来覆盖这些注册表设置。 更好的方法是，驱动程序在安装时确定特定驱动程序特定的注册表项是否已存在。 如果它们存在，驱动程序应保留这些项中包含的设置，而不是覆盖这些项。

驱动程序 INF 文件的 "添加注册表" 部分中的指令指定是否应覆盖现有的注册表项。 有关详细信息，请参阅 FLG \_ ADDREG \_ NOCLOBBER Flag In [**INF ADDREG 指令**](../install/inf-addreg-directive.md)中的说明。

### <a name="span-idmigration_dllspanspan-idmigration_dllspanspan-idmigration_dllspanmigration-dll"></a><span id="Migration_DLL"></span><span id="migration_dll"></span><span id="MIGRATION_DLL"></span>迁移 DLL

在从 Windows Me/98 升级到基于 NT 的操作系统 (Windows 2000 和更高版本中) ，Windows 安装程序会将 Windows Me/98 下安装的设备驱动程序视为不兼容，并放弃驱动程序和其注册表设置。

此外，如果 Windows 2000 安装程序找不到设备的内置驱动程序支持，程序会立即提示用户提供驱动程序软件。 在 Windows XP 和更高版本中，如果安装程序找不到适合的驱动程序或在 Windows 更新站点上，则将等待升级完成，通知用户缺少驱动程序。

尽管驱动程序在此类升级过程中无法避免其注册表设置丢失，但 Microsoft 建议使用迁移 DLL 以透明方式为用户重新安装兼容的驱动程序。 为此，Microsoft 提供了 Devupgrd 迁移 DLL，该 DLL 包含在 Windows 驱动程序工具包 (WDK) 的安装即插即用示例中。 该示例包含一个描述迁移 DLL 的帮助文件。

迁移 DLL 只能与最初安装在 Windows Me/98 下的 WDM 驱动程序一起使用，但也可以在 Windows 2000 或 Windows XP 上运行。 请注意，迁移 DLL 无法将驱动程序从 Windows Me/98 升级到 Windows Server 2003、Windows Vista 或更高版本。 它只能将驱动程序从 Windows Me/98 升级到 Windows XP 或 Windows 2000。

在从 Windows Me/98 升级到 Windows XP 或 Windows 2000 期间，迁移 DLL 会执行以下操作：

-   从设备驱动程序的位置在 Windows Me/98 注册表中读取设备驱动程序的迁移信息。

-   向驱动程序的 INF 文件添加必要的信息，以确保在 Windows XP 或 Windows 2000 下正确安装设备。

要使迁移信息以后可用于 Windows XP 或 Windows 2000 安装程序，在 Windows Me/98 下安装设备的 INF 文件应执行以下操作：

-   将迁移 DLL 复制到 INF 指定的备份目录，并将该目录的路径名称添加到 Windows Me/98 注册表。

-   向注册表添加标识可以迁移的设备的设备 Id。

-   将设备驱动程序文件)  ( 的备份副本保存到 INF 指定的备份目录中，并将这些目录的路径名添加到注册表。

在升级过程中，Windows XP 或 Windows 2000 安装程序会将备份目录名称添加到已注册设备 Id 的 INF 搜索路径中。

如上所述，在从 Windows Me/98 升级到 Windows XP 或 Windows 2000 期间，安装程序会丢弃驱动程序的注册表设置。 使用迁移 DLL 的帮助执行的驱动程序重新安装是 "全新安装"，其中，驱动程序的卷、静音和其他设置均采用其初始的默认值。

Windows 驱动程序工具包 (WDK) 中的 Ac97 音频适配器示例包含一个 INF 文件示例， (Ac97smpl) 将音频驱动程序从 Windows Me/98 迁移到 Windows XP 或 Windows 2000。

 

