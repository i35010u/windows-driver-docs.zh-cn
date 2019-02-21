---
title: APN 数据库概述
description: APN 数据库概述
ms.assetid: 699b797e-c225-47ba-96a5-26b15c91a759
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70450eca7688c90045326ca12bd76c04309204d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555427"
---
# <a name="apn-database-overview"></a>APN 数据库概述

APN 数据库或 apndatabase.xml，移动操作员 (MOs) 使用配置为其网络的移动宽带体验的预配数据库。 它现已推出 Windows 8、 Windows 8.1 和 Windows 10 版本 1703年的 Windows 10 之前的版本。

从 Windows 10，版本 1703，开始 APN 数据库将替换为新格式称为 COSA。 Windows 8、 Windows 8.1 和 Windows 10 版本 1703年将继续使用 APN 数据库存在时 Windows 10 之前的版本，版本 1703年及更高版本使用 COSA。 

有关 COSA 的详细信息，请参阅[COSA 概述](cosa-overview.md)。

若要查看 MOs 可以配置 APN 数据库中的可用设置的列表，请参阅[桌面 COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

## <a name="span-idapndbconspanspan-idapndbconspanapn-database-contents"></a><span id="apndbcon"></span><span id="APNDBCON"></span>APN 数据库内容


若要连接到移动宽带网络，用户通常提供以下信息：

- 在全局系统中的移动通信 (GSM) 网络，例如 APN **data.contoso.com**。

- 在 CDMA 网络包括一个特殊的访问字符串拨打代码如 **\#777**，或如网络访问标识符 (NAI) <strong>ann@contoso.com</strong>。

- 用户的凭据 （用户名和密码） 的网络连接。

具体而言，APN 数据库包括以下数据：

-   **运算符的身份验证数据**

    -   对于 GSM 网络，你可以提交的国际移动 (IMSI) 或您的网络使用的集成线路卡标识符 (ICCID) 范围的数据库条目。 如果要移动的虚拟网络运营商 (MVNO)，可以指定一个或多个范围的 IMSIs 或订阅服务器上标识模块 (SIM) ICC 从移动网络运营商 (MNO) 租用的 Id。

    -   对于 CDMA 网络，可以为每个提供程序 ID 或提供程序名称来提交新的数据库条目。

    -   若要更好地了解如何标识 Mvno，请参阅[交付体验来 Mvno](delivering-experiences-for-mvnos.md)。

-   **购买 APNs 的列表，以及访问字符串**

    -   对于 GSM 网络，APNs 具有用户名和密码才能购买订阅的列表。

    -   对于 CDMA 网络，NAIs 购买订阅的列表。

-   **列表中的 Internet 连接 APNs 和访问字符串**

    -   对于 GSM 网络，具有用户名和密码以连接到 Internet 的 APNs 的列表。

    -   对于 CDMA 网络，用于连接到 Internet 的 NAIs 的列表。

-   **帐户体验 URL**首次购买帐户 URL 体验 web 站点。

-   **证书数据**证书帐户预配的元数据的信息。 这包括证书颁发者名称和使用者名称和用于验证帐户预配附带的采购网站来自用户的被授权 web 服务。

APN 数据库 XML 架构的详细信息，请参阅[APN 数据库架构参考](apn-database-schema-reference.md)。

## <a name="span-idabndbsubspanspan-idabndbsubspanapn-database-submission-and-maintenance"></a><span id="abndbsub"></span><span id="ABNDBSUB"></span>APN 数据库提交和维护


如果你想要请求新 APN 或更新现有的一个，请参阅[COSA/APN 数据库提交](cosa-apn-database-submission.md)。
 





