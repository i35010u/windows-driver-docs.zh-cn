---
title: NDIS 筛选器驱动程序安装
description: NDIS 筛选器驱动程序安装
ms.assetid: 8e0c47bf-6b63-4be5-98b7-7a99e9efe283
keywords:
- 筛选器驱动程序 WDK 网络，安装
- NDIS 筛选器驱动程序 WDK，安装
- 安装 NDIS 筛选器驱动程序 WDK 网络
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: d26b4a9be24da160fc7da9fd1417c2690b16755c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211771"
---
# <a name="ndis-filter-driver-installation"></a>NDIS 筛选器驱动程序安装

本部分提供有关安装 NDIS 筛选器驱动程序的信息。 轻型筛选器驱动程序不同于筛选器中间驱动程序。 配置管理器向 NDIS 提供每个微型端口适配器的筛选器模块列表。 没有与筛选器驱动程序相关联的虚拟设备 (或虚拟微型端口) 与 NDIS 筛选器中间驱动程序相同。

若要安装筛选器驱动程序，必须提供一个 INF 文件。 配置管理器从 INF 文件中读取有关筛选器驱动程序的配置信息，并将其复制到注册表。

筛选器驱动程序 INF 文件定义了网络服务。 筛选器驱动程序没有微型端口 INF 文件。 有关筛选器驱动程序 INF 文件示例，请参阅 [ndislwf](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/filter) 示例驱动程序。

提供筛选器驱动程序 INF 文件后，若要安装或卸载筛选器驱动程序，必须使用 `INetCfg` 系列的 [网络配置接口](/previous-versions/windows/hardware/network/ff559080(v=vs.85))。 例如，若要安装或删除网络组件，请调用 [INetCfgClassSetup](/previous-versions/windows/hardware/network/ff547709(v=vs.85)) 接口。 您可以通过编程方式调入这些接口，也可以通过 [netcfg.exe](/windows-server/administration/windows-commands/netcfg)来间接调用它们，这会 `INetCfg` 为您调用。 不能使用 [setupapi.log](../install/setupapi.md) 来安装或卸载 NDIS 筛选器驱动程序。

有关通过代码调用的示例 `INetCfg` ，请参阅 [Bindview 网络配置实用工具示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/config/bindview)。

本节包括：

[指定筛选器驱动程序绑定关系](specifying-filter-driver-binding-relationships.md)

[筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)

[访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)