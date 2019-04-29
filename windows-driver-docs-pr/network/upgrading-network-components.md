---
title: 网络组件的升级过程
description: 网络组件的升级过程
ms.assetid: ddd1eda0-7bed-44e7-8636-8db3508825f5
keywords:
- 网络组件升级 WDK
- 升级网络组件 WDK
- 有关升级网络组件的网络组件升级 WDK，
- 有关升级网络组件升级网络组件 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc22be488ce1facd2e0fa35afdc31da0b01fe45f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387147"
---
# <a name="process-for-upgrading-network-components"></a>网络组件的升级过程





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (Service Pack 1 \[SP1\]及更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

网络升级过程将操作系统升级过程中迁移网络组件的参数值。 网络升级过程因此消除了需要安装新操作系统后，重新配置已升级的网络组件。

网络升级过程会从 Microsoft Windows NT 3.51 或 Windows NT 4.0 网络组件升级到 Microsoft Windows 2000 或更高版本的操作系统。 网络升级过程不会升级网络组件从 Windows 2000 到更高版本的操作系统中。

Windows 2000 或更高版本的一部分应通过提供以下有关这些组件提供升级支持，也不会释放其网络组件的供应商：

-   网络迁移迁移一个或多个网络组件的升级前的参数值的 DLL。

-   映射到新操作系统中的相应 ID 的升级前的设备、 硬件或兼容 ID 的一个或多个网络组件 netmap.inf 文件。

-   可选自定义帮助消息文件提供有关升级网络组件的信息。

以下主题介绍了网络升级过程：

[自定义网络升级过程](customizing-the-network-upgrade-process.md)

[网络升级过程](the-network-upgrade-process.md)

[编写网络迁移 DLL](writing-a-network-migration-dll.md)

[创建 Netmap.inf 文件](creating-a-netmap-inf-file.md)

[测试升级网络组件](testing-the-upgrade-of-network-components.md)

安装操作系统时，将自动升级其驱动程序将发布为 Windows 2000 或更高版本操作系统的一部分的网络组件。 不支持其他升级是必需的此类组件。

 

 





