---
title: NDIS 协议驱动程序安装
description: NDIS 协议驱动程序安装
ms.assetid: D783E386-91A2-4E6E-8340-78E0FFA14974
keywords:
- 协议驱动程序 WDK 网络，安装
- NDIS 协议驱动程序 WDK，安装
- 安装 NDIS 协议驱动程序 WDK 网络
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: b5b4384dfefa4e3bf9b39107385ee521f35dcd0e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211755"
---
# <a name="ndis-protocol-driver-installation"></a>NDIS 协议驱动程序安装

若要安装协议驱动程序，必须先提供一个 INF 文件。 配置管理器从 INF 文件中读取有关协议驱动程序的配置信息，并将其复制到注册表。 

有关协议驱动程序 INF 文件的详细信息，请参阅 [网络协议的安装要求](installation-requirements-for-network-protocols.md)。 有关协议驱动程序 INF 文件的示例，请参阅 [ndisprot 630](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/ndisprot/6x/sys/630) 示例驱动程序。

提供协议驱动程序 INF 文件后，若要安装或卸载协议驱动程序，必须使用 `INetCfg` 系列的 [网络配置接口](/previous-versions/windows/hardware/network/ff559080(v=vs.85))。 例如，若要安装或删除网络组件，请调用 [INetCfgClassSetup](/previous-versions/windows/hardware/network/ff547709(v=vs.85)) 接口。 您可以通过编程方式调入这些接口，也可以通过 [netcfg.exe](/windows-server/administration/windows-commands/netcfg)来间接调用它们，这会 `INetCfg` 为您调用。 不能使用 [setupapi.log](../install/setupapi.md) 来安装或卸载 NDIS 协议驱动程序。

有关通过代码调用的示例 `INetCfg` ，请参阅 [Bindview 网络配置实用工具示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/config/bindview)。