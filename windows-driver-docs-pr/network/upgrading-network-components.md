---
title: 网络组件的升级过程
description: 网络组件的升级过程
keywords:
- 网络组件升级 WDK
- 升级网络组件 WDK
- 网络组件升级 WDK，关于升级网络组件
- 升级网络组件 WDK，关于升级网络组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 630222f32bc10658881290af30d80ee6d3c05250
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809911"
---
# <a name="process-for-upgrading-network-components"></a>网络组件的升级过程





**注意**  Microsoft Windows XP (Service Pack 1 \[ SP1 \] 及更高版本) 、Microsoft windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

网络升级过程在操作系统升级过程中迁移网络组件的参数值。 因此，网络升级过程不再需要在安装新操作系统之后重新配置升级的网络组件。

网络升级过程将网络组件从 Microsoft Windows NT 3.51 或 Windows NT 4.0 升级到 Microsoft Windows 2000 或更高版本的操作系统。 网络升级过程不会将网络组件从 Windows 2000 升级到更高版本的操作系统。

其网络组件未在 Windows 2000 或更高版本中发布的供应商应通过提供以下内容为这些组件提供升级支持：

-   为一个或多个网络组件迁移 preupgrade 参数值的网络迁移 DLL。

-   将一个或多个网络组件的 preupgrade 设备、硬件或兼容 ID 映射到新操作系统中相应 ID 的 netmap 文件。

-   可选的自定义帮助消息文件，提供有关升级网络组件的信息。

以下主题介绍了网络升级过程：

[自定义网络升级过程](customizing-the-network-upgrade-process.md)

[网络升级过程](the-network-upgrade-process.md)

[编写网络迁移 DLL](writing-a-network-migration-dll.md)

[创建 Netmap.inf 文件](creating-a-netmap-inf-file.md)

测试网络组件的升级涉及两个主要步骤。 以下主题介绍了这些内容：

[设置测试系统](setting-up-the-test-system.md)

[运行升级测试并检查结果](running-the-upgrade-test-and-examining-the-results.md)

安装操作系统时，会自动升级其驱动程序作为 Windows 2000 或更高版本操作系统的一部分发布的网络组件。 此类组件不需要其他升级支持。

 

 





