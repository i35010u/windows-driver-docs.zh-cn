---
title: 安装微筛选器驱动程序
description: 安装微筛选器驱动程序
ms.assetid: c31aa104-404e-43e3-9215-2671ae6b12c0
keywords:
- 文件系统微筛选器驱动程序 WDK，安装
- 微筛选器驱动程序 WDK，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84f6254a9aa27f95f70e2f14db4f066e4ff3dd73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370123"
---
# <a name="installing-a-minifilter-driver"></a>安装微筛选器驱动程序


对于 Microsoft Windows XP 和更高版本操作系统，应使用 INF 文件和安装应用程序来安装微筛选器驱动程序。 （在 Windows 2000 和更早的操作系统，微筛选器驱动程序通常安装的服务控制管理器。）

将来，有必要以符合微筛选器驱动程序的 Windows 硬件认证工具包要求应基于 INF 的安装。 请注意，"基于 INF 的安装"仅意味着需要使用 INF 文件以将文件复制并存储在注册表中的信息。 您不需要在使用仅的 INF 文件，请安装整个产品和你不将需要提供["右键单击安装"](using-an-inf-file-to-install-a-file-system-filter-driver.md)您的驱动程序的选项。

本部分包括：

[创建用于微筛选器驱动程序的 INF 文件](creating-an-inf-file-for-a-minifilter-driver.md)

[加载顺序组和海拔微筛选器驱动程序的地区](load-order-groups-and-altitudes-for-minifilter-drivers.md)

[已分配的海拔地区](allocated-altitudes.md)

[微筛选器海拔高度请求](minifilter-altitude-request.md)

[重新分析点标记请求](reparse-point-tag-request.md)

 

 




