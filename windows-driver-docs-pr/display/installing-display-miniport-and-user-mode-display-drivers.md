---
title: 安装显示微型端口和用户模式显示驱动程序
description: 显示微型端口和用户模式显示驱动程序的安装要求
ms.assetid: f813071d-897d-4100-bc46-326558de2e70
keywords:
- 显示驱动程序模型 WDK Windows Vista 中，驱动程序安装
- Windows Vista 显示器驱动程序模型 WDK，驱动程序安装
- 显示驱动程序模型 WDK Windows Vista 安装
- 用户模式驱动程序 WDK 显示
- INF 文件 WDK 显示
- 图形设备显示微型端口驱动程序 WDK Windows Vista
- INF 文件 WDK 显示有关驱动程序安装
- 微型端口驱动程序 WDK 显示，请安装
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d477e0f5fa1da4ace403258679f4a2a3af74050c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379903"
---
# <a name="installation-requirements-for-display-miniport-and-user-mode-display-drivers"></a>显示微型端口和用户模式显示驱动程序的安装要求


使用 INF 文件标记为在操作系统上安装图形设备显示微型端口驱动程序**类 = 显示**。 在驱动程序安装过程中，将由系统提供显示类安装程序解释此 INF。

图形设备显示微型端口驱动程序适用于 Windows Vista 及更高版本的 INF 文件必须存储下的所有软件设置[ **DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。 这样做会导致操作系统将所有注册表值复制 (PnP) 插到软件密钥在注册表中。

若要确保正确安装，必须符合对 Windows 显示驱动程序模型 (WDDM) 任何显示微型端口驱动程序的 INF 文件中提供以下信息。

[设置驱动程序控制标志](setting-the-driver-control-flags.md)

[添加软件注册表设置](adding-software-registry-settings.md)

[将用户模式显示驱动程序名称添加到注册表](adding-user-mode-display-driver-names-to-the-registry.md)

[正在加载用户模式显示驱动程序](loading-a-user-mode-display-driver.md)

[设置驱动程序功能分数](setting-the-driver-feature-score.md)

[设置复制文件标志来支持即插即用停止](setting-a-copy-file-flag-to-support-pnp-stop.md)

[设置起始类型值](setting-the-start-type-value.md)

[禁用与 OpenGL 互操作性](disabling-interoperability-with-opengl.md)

[将信息追加到的图形适配器的友好字符串名称](appending-information-to-the-friendly-string-names-of-graphics-adapter.md)

[忽略 LayoutFile 和 CatalogFile 信息](omitting-layoutfile-and-catalogfile-information.md)

[标识源磁盘和文件](identifying-source-disks-and-files.md)

[常规 x 64 INF 信息](general-x64-inf-information.md)

[常规安装信息](general-install-information.md)

[重写使用 INF 监视器 EDIDs](overriding-monitor-edids.md)

应参考[INF 文件概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)并[INF 文件的部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)的部分，了解在创建了显示微型端口驱动程序 INF 文件的常规帮助。 详细了解注册表根的标识符，如**HKR**，请参阅[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

**请注意**  有没有 INF 部分和卸载指令显示特定于图形设备的驱动程序。

 

 

 





