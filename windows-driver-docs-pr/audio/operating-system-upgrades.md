---
title: 操作系统升级
description: 操作系统升级
ms.assetid: f985967e-e6cf-431a-bb7e-7b6d8486709c
keywords:
- 音频适配器 WDK，操作系统升级
- 适配器驱动程序 WDK 音频，操作系统升级
- 端口类音频适配器 WDK，操作系统升级
- 保留音频设置 WDK 音频
- 迁移 DLL WDK 音频
- 迁移设置 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6867e25d64d7e287d66ee04fffd96bc2474cb3ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532945"
---
# <a name="operating-system-upgrades"></a>操作系统升级


## <span id="operating_system_upgrades"></span><span id="OPERATING_SYSTEM_UPGRADES"></span>


经常可以在操作系统升级保留音频设备的驱动程序和注册表设置。 下面的论述中提供了实现此目的一些指导的原则。

### <a name="span-idpreservingaudiosettingsspanspan-idpreservingaudiosettingsspanspan-idpreservingaudiosettingsspanpreserving-audio-settings"></a><span id="Preserving_Audio_Settings"></span><span id="preserving_audio_settings"></span><span id="PRESERVING_AUDIO_SETTINGS"></span>保留音频设置

音频适配器驱动程序可以跟踪的其当前的设备设置--chiefly 音量级别，并将调节到静音设置--在系统注册表中。 该驱动程序通常将这些设置存储在子项"设置"下的系统提供的驱动程序键 （由 INF 关键字 HKR）。 当用户更改这些设置通过控制面板或其他音频的应用程序时，该驱动程序更新相应的注册表项。 在系统引导时，每次该驱动程序，从注册表还原的设备设置。

从 Windows 升级我时 / 98 到 Windows XP 或 Windows 2000 中的，Windows 安装程序是不能保留这些设置。

但是，当升级从 Windows 在我看来，Windows 98 或从一个基于 NT 的操作系统 （例如，从 Windows 2000 到 Windows XP) 到另一个，安装程序使驱动程序的现有注册表设置保持不变。 用户很大程度上更喜欢这种行为，因为它将保留对进行了系统随时间而不是强制它们可尝试手动升级操作系统，他们每次恢复其设置的调整。

某些专有的驱动程序，但是，会盲目地覆盖这些注册表设置使用默认值每次安装它们。 更好的方法是驱动程序以在安装时确定是否某些驱动程序特定的注册表项已存在。 如果它们存在，该驱动程序应保留而不是覆盖它们这些项中包含的设置。

驱动程序的 INF 文件的添加注册表部分中的指令指定是否应覆盖现有的注册表项。 有关详细信息，请参阅说明 FLG\_ADDREG\_中的 NOCLOBBER 标志[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。

### <a name="span-idmigrationdllspanspan-idmigrationdllspanspan-idmigrationdllspanmigration-dll"></a><span id="Migration_DLL"></span><span id="migration_dll"></span><span id="MIGRATION_DLL"></span>迁移 DLL

从 Windows 升级期间我 / 98 到基于 NT 的操作系统 (Windows 2000 及更高版本)，Windows 安装程序将设备驱动程序已在 Windows 下安装我 / 98 为不兼容，然后放弃该驱动程序和其注册表设置。

此外，如果 Windows 2000 安装程序发现设备不现成驱动程序支持，程序将立即提示用户提供的驱动程序软件。 在 Windows XP 及更高版本，如果找不到适当的驱动程序，在框或 Windows Update 站点上安装程序，它会等到完成升级以通知用户缺少的驱动程序。

尽管驱动程序不能在此类升级期间避免丢失其注册表设置，但 Microsoft 建议迁移 DLL 重新安装兼容的驱动程序对用户是透明的使用。 为此，Microsoft 提供了 Devupgrd 迁移 DLL，包含在安装即插即用和播放示例 Windows Driver Kit (WDK) 中。 此示例包括描述迁移 DLL 的帮助文件。

仅对于最初的 WDM 驱动程序应使用 DLL 的迁移在 Windows 下安装我 / 98 但也是能够在 Windows 2000 或 Windows XP 上运行。 请注意，迁移 DLL 不能升级驱动程序从 Windows Me / 98 到 Windows Server 2003，Windows Vista 或更高版本。 它可以只升级驱动程序从 Windows Me / 98 到 Windows XP 或 Windows 2000。

在从 Windows 升级过程中我 / 98 到 Windows XP 或 Windows 2000，迁移 DLL 执行以下操作：

-   我从 Windows 中的位置读取设备驱动程序的迁移信息 / 98 注册表。

-   将所需的信息添加到驱动程序的 INF 文件，以确保设备在 Windows XP 或 Windows 2000 下正确安装。

若要将 Windows XP 或 Windows 2000 安装程序的 INF 文件到更高版本提供的迁移信息用于安装在 Windows 设备我/98 应执行以下操作：

-   将迁移 DLL 复制到 INF 指定备份目录和该目录的路径将名称添加到 Windows Me / 98 注册表。

-   向注册表添加设备识别可迁移的设备的 Id。

-   将设备的备份副本保存到 INF 指定备份目录的驱动程序文件 （.sys 和.inf） 并将这些目录的路径名称添加到注册表。

在升级期间，Windows XP 或 Windows 2000 安装程序将备份目录名称添加到已注册的设备 Id 的 INF 搜索路径。

如上文所述，安装程序将放弃驱动程序的注册表设置从 Windows 升级期间我 / 98 到 Windows XP 或 Windows 2000。 重新安装驱动程序的 DLL 帮助执行是迁移的"clean install"驱动程序的卷、 静音，以及其他设置假定其初始，默认值。

Ac97 音频适配器示例 Windows Driver Kit (WDK) 中包含的 INF 文件 (Ac97smpl.inf)，我从 Windows 迁移音频驱动程序的示例 / 98 到 Windows XP 或 Windows 2000。

 

 




