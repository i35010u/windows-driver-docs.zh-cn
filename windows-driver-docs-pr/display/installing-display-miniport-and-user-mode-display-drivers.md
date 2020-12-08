---
title: 安装显示器微型端口和 User-Mode 显示器驱动程序
description: 显示微型端口和用户模式显示驱动程序的安装要求
keywords:
- 显示驱动程序模型 WDK Windows Vista，驱动程序安装
- Windows Vista 显示器驱动程序模型 WDK，驱动程序安装
- 显示驱动程序模型 WDK Windows Vista，安装
- 用户模式驱动程序 WDK 显示
- INF 文件 WDK 显示
- 图形设备显示器微型端口驱动程序 WDK Windows Vista
- INF 文件 WDK 显示，关于驱动程序安装
- 微型端口驱动程序 WDK 显示，安装
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: cc500cdce3654dd1446c2cd497185d723b62b60d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827217"
---
# <a name="installation-requirements-for-display-miniport-and-user-mode-display-drivers"></a>显示微型端口和用户模式显示驱动程序的安装要求


通过使用标记为 " **类 = 显示**" 的 INF 文件在操作系统上安装图形设备的显示微型端口驱动程序。 系统提供的显示类安装程序会在驱动程序安装过程中解释此 INF。

对于 Windows Vista 和更高版本，图形设备的显示微型端口驱动程序的 INF 文件必须在 [**DDInstall 节**](../install/inf-ddinstall-section.md)下存储所有软件设置。 这样做会导致操作系统将注册表中的所有注册表值复制到即插即用 (PnP) 软件密钥。

若要确保正确安装，必须在任何符合 Windows 显示器驱动程序模型 (WDDM) 的显示微型端口驱动程序的 INF 文件中提供以下信息。

[设置驱动程序控制标志](setting-the-driver-control-flags.md)

[添加软件注册表设置](adding-software-registry-settings.md)

[将用户模式显示驱动程序名称添加到注册表](adding-user-mode-display-driver-names-to-the-registry.md)

[加载用户模式显示驱动程序](loading-a-user-mode-display-driver.md)

[设置驱动程序功能评分](setting-the-driver-feature-score.md)

[设置 Copy-File 标志以支持 PnP 停止](setting-a-copy-file-flag-to-support-pnp-stop.md)

[设置启动类型值](setting-the-start-type-value.md)

[禁用 OpenGL 互操作性](disabling-interoperability-with-opengl.md)

[将信息追加到图形适配器的友好字符串名称](appending-information-to-the-friendly-string-names-of-graphics-adapter.md)

[省略 LayoutFile 和 CatalogFile 信息](omitting-layoutfile-and-catalogfile-information.md)

[识别源磁盘和文件](identifying-source-disks-and-files.md)

[常规 x64 INF 信息](general-x64-inf-information.md)

[常规安装信息](general-install-information.md)

[使用 INF 替代监视器 Edid](overriding-monitor-edids.md)

有关创建显示微型端口驱动程序 INF 文件的常规帮助，请参阅 [Inf 文件](../install/overview-of-inf-files.md) 和 [inf 文件部分和指令](../install/index.md) 部分的概述。 有关注册表根标识符（如 **HKR**）的详细信息，请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)。

**注意**   没有用于卸载特定于图形设备的显示驱动程序的 INF 部分和指令。

 

