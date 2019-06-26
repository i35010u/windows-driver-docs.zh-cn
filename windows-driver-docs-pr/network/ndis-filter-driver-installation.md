---
title: NDIS 筛选器驱动程序安装
description: NDIS 筛选器驱动程序安装
ms.assetid: 8e0c47bf-6b63-4be5-98b7-7a99e9efe283
keywords:
- 筛选器驱动程序 WDK 网络安装
- NDIS 筛选器驱动程序 WDK，安装
- 正在安装 NDIS 筛选器驱动程序 WDK 网络
ms.date: 01/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: af7bf0f647c69d844e767124001d4d92db176574
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369625"
---
# <a name="ndis-filter-driver-installation"></a>NDIS 筛选器驱动程序安装

本部分提供有关安装 NDIS 筛选器驱动程序的信息。 轻型筛选器驱动程序是不同于筛选器中间驱动程序。 配置管理器向 NDIS 提供的每个微型端口适配器的筛选器模块的列表。 没有任何虚拟设备 （或虚拟微型端口），因为没有使用 NDIS 筛选器中间驱动程序是与筛选器驱动程序相关联。

若要安装的筛选器驱动程序，必须提供一个单一的 INF 文件。 Configuration manager 从 INF 文件中读取有关筛选器驱动程序的配置信息，并将其复制到注册表。

筛选器驱动程序 INF 文件定义的网络服务。 筛选器驱动程序不具备微型端口 INF 文件。 有关筛选器驱动程序 INF 文件示例，请参阅[ndislwf](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/filter)示例驱动程序。

提供筛选器驱动程序 INF 文件中，以安装或卸载您必须使用的筛选器驱动程序后`INetCfg`系列[网络配置接口](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559080(v=vs.85))。 例如，若要安装或删除网络组件，调入[INetCfgClassSetup](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547709(v=vs.85))接口。 以编程方式可以为这些接口调用或间接调用与它们[netcfg.exe](https://docs.microsoft.com/windows-server/administration/windows-commands/netcfg)，它调用`INetCfg`为您。 不能使用[SetupAPI](../install/setupapi.md)安装或卸载 NDIS 筛选器驱动程序。

有关调用的示例`INetCfg`通过代码，请参阅[Bindview 网络配置实用工具示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/config/bindview)。

本部分包括：

[指定绑定的关系的筛选器驱动程序](specifying-filter-driver-binding-relationships.md)

[筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)

[访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)