---
title: NDIS 协议驱动程序安装
description: NDIS 协议驱动程序安装
ms.assetid: D783E386-91A2-4E6E-8340-78E0FFA14974
keywords:
- 协议驱动程序 WDK 网络安装
- NDIS 协议驱动程序 WDK，安装
- 正在安装 NDIS 协议驱动程序 WDK 网络
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7c7eca1e6a2c3a86dec3bfae3992877d4398879f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545061"
---
# <a name="ndis-protocol-driver-installation"></a>NDIS 协议驱动程序安装

若要安装协议驱动程序，必须先提供一个 INF 文件。 Configuration manager 从 INF 文件中读取有关协议驱动程序的配置信息，并将其复制到注册表。 

有关协议驱动程序 INF 文件的详细信息，请参阅[的网络协议的安装要求](installation-requirements-for-network-protocols.md)。 有关示例协议驱动程序 INF 文件，请参阅[ndisprot 630](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot/6x/sys/630)示例驱动程序。

提供协议驱动程序 INF 文件中，以安装或卸载您必须使用的协议驱动程序后`INetCfg`系列[网络配置接口](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v%3dvs.85))。 例如，若要安装或删除网络组件，调入[INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709%28v%3dvs.85%29)接口。 以编程方式可以为这些接口调用或间接调用与它们[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)，它调用`INetCfg`为您。 不能使用[SetupAPI](../install/setupapi.md)安装或卸载 NDIS 协议驱动程序。

有关调用的示例`INetCfg`通过代码，请参阅[Bindview 网络配置实用工具示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/config/bindview)。