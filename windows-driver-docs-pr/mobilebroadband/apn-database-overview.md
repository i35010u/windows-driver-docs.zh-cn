---
title: APN 数据库概述
description: APN 数据库概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 520e101d39529135cb643dbc5803576c3229df9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782549"
---
# <a name="apn-database-overview"></a>APN 数据库概述

APN 数据库或 apndatabase.xml 是移动运营商 (MOs) 用来为其网络配置移动宽带体验的预配数据库。 Windows 8、Windows 8.1 和 windows 10 版本1703之前的版本中提供了该功能。

从 Windows 10 版本1703开始，APN 数据库被称为 COSA 的新格式所取代。 Windows 10 版本1703之前的 windows 8、Windows 8.1 和版本将继续使用 APN 数据库，Windows 10 版本1703及更高版本都使用 COSA。 

有关 COSA 的详细信息，请参阅 [COSA 概述](cosa-overview.md)。

若要查看 MOs 可以在 APN 数据库中配置的可用设置的列表，请参阅 [DESKTOP COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

## <a name="span-idapndbconspanspan-idapndbconspanapn-database-contents"></a><span id="apndbcon"></span><span id="APNDBCON"></span>APN 数据库内容


若要连接到移动宽带网络，用户通常提供以下信息：

- 在移动通信的全球系统中 (GSM) 网络、 **data.contoso.com** 等接入点。

- 在 CDMA 网络中，包含特殊拨号代码（如 **\# 777**）的访问字符串，或 (NAI) 的网络访问标识符（如） <strong>ann@contoso.com</strong> 。

- 用户的凭据 (网络连接的用户名和密码) 。

具体而言，APN 数据库包含以下数据：

-   **操作员标识数据**

    -   对于 GSM 网络，可以提交国际移动用户标识 (IMSI) 或集成卡标识符 (网络使用的 ICCID) 范围的数据库条目。 如果你是 (MVNO) 的移动虚拟网络运营商，则可以指定一个或多个 IMSIs 或订阅服务器标识模块的范围 (SIM) 你从移动网络运营商那里租赁的 SIM Id (o) 。

    -   对于 CDMA 网络，你可以为每个提供程序 ID 或提供程序名称提交新的数据库条目。

    -   若要更好地了解如何识别 Mvno，请参阅 [为 Mvno 提供体验](delivering-experiences-for-mvnos.md)。

-   **采购 APNs 和访问字符串列表**

    -   对于 GSM 网络，为一个 APNs 列表，其中包含用于购买订阅的用户名和密码。

    -   对于 CDMA 网络，为购买订阅的 NAIs 列表。

-   **Internet 连接 APNs 和访问字符串列表**

    -   对于 GSM 网络，为使用用户名和密码连接到 Internet 的 APNs 列表。

    -   对于 CDMA 网络，是用于连接到 Internet 的 NAIs 列表。

-   **帐户体验 URL** 第一次购买帐户体验网站的 URL。

-   **证书数据** 帐户预配元数据的证书信息。 这包括证书颁发者名称和使用者名称，并用于验证购买网站提供的帐户设置是否来自用户的授权 web 服务。

有关 APN 数据库 XML 架构的详细信息，请参阅 [apn 数据库架构参考](apn-schema-definition.md)。

## <a name="span-idabndbsubspanspan-idabndbsubspanapn-database-submission-and-maintenance"></a><span id="abndbsub"></span><span id="ABNDBSUB"></span>APN 数据库提交和维护


如果要请求新接入点或更新现有接入点，请参阅 [COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。
 





