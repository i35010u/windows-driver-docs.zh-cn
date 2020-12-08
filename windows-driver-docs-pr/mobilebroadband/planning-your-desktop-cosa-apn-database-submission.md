---
title: 规划桌面 COSA/APN 数据库提交
description: 规划桌面 COSA/APN 数据库提交
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8564cd59ff17a620b08414fb4c25551f0ab6dadd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786209"
---
# <a name="planning-your-desktop-cosaapn-database-submission"></a>规划桌面 COSA/APN 数据库提交

> [!IMPORTANT]
> 从 Windows 10 版本1703开始，APN 数据库被称为 COSA 的新格式所取代。 Windows 10 版本1703之前的 windows 8、Windows 8.1 和版本将继续使用 APN 数据库，Windows 10 版本1703及更高版本都使用 COSA。 有关 COSA 的详细信息，请参阅 [COSA 概述](cosa-overview.md)。

当你计划将新的 APN 添加到随 Windows 桌面设备附带的基线 COSA/APN 数据库时，请使用本主题中的部分，或者更新现有接入点。

## <a name="the-apn-update-process"></a>APN 更新过程

若要连接到移动宽带网络，通常需要用户提供以下信息：

- 在 GSM 网络上，访问点名称 (APN) 例如 "data.contoso.com"。

- 在 CDMA 网络上，需要一个包含特殊拨号代码（如 "777"）的访问字符串 \# 或网络访问标识符（如） somebody@contoso.com 。

- 网络连接的用户名和密码。

COSA 和 APN 连接数据库通过使用 Windows 更新进行更新。 下图显示了整个提交过程。

![COSA/APN 数据库提交过程](images/COSA_and_APN_database_submission_process_diagram.png "COSA/APN 数据库提交过程")

## <a name="complete-the-apncosa-update-spreadsheet"></a>完成 APN/COSA 更新电子表格

接入点更新电子表格用于收集所需的信息，以便 Microsoft 可以相应地更新 COSA 或 APN 数据库。 你向 Microsoft 提交的请求中包含此电子表格。 提交 APN 更新时，MOs 应将所有信息发送到 Microsoft，以将所有设备定向到 Microsoft。

使用以下链接下载最新的 APN 更新电子表格： <https://go.microsoft.com/fwlink/p/?linkid=851213>

有关 APN 更新电子表格中的设置的详细信息，请参阅 [DESKTOP COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

## <a name="considerations-when-completing-the-spreadsheet"></a>完成电子表格时的注意事项

### <a name="apn-database-considerations"></a>APN 数据库注意事项

仅当使用 apndatabase.xml （对于 windows 8、Windows 8.1 或 windows 10 版本1703之前的版本）提交 APN 更新时，请注意以下各项。

- 操作员标识数据以编码的硬件 Id 的形式存储在 APN 数据库中。
  -   对于 GSM 网络，可以为 MCC/MNC 对的每个唯一组合提供单独的数据库条目。 如果你是 (MVNO) 的移动虚拟网络运营商，并且没有唯一的 MCC/MNC 对，则可以指定当前从移动网络操作员 (o) 租赁的一个或多个 IMSIs 或 SIM ICC Id 的范围。
  -   对于 CDMA 网络，你可以为每个提供程序 ID 提供一个新的数据库条目 (也称为 SID) 或提供程序名称。
  -   帐户预配元数据的证书信息包括 **证书颁发者名称** 和 **证书使用者名称** ，并用于验证购买网站提供的帐户预配是否来自授权 web 服务。 如果此处存储的证书信息与购买网站的内容相匹配，则 Windows 将允许该网站将网络特定的配置信息推送到 PC。

- 使用 apndatabase.xml 提交 APN 数据库更新时，必须包括以下值：       
    - CDMA 提供程序名称
    - SID (的 CDMA 提供程序 ID) 

- 帐户预配元数据的证书信息包括 **证书颁发者名称** 和 **证书使用者名称** ，并用于验证购买网站提供的帐户预配是否来自授权 web 服务。 如果此处存储的证书信息与购买网站的内容相匹配，则 Windows 将允许该网站将网络特定的配置信息推送到 PC。 

- 对于 **运算符** 和 **国家/地区** 组合，自动连接顺序必须是唯一的，且必须具有相同的 IMSI、ICCID 范围、CDMA 提供程序名称或 CDMA 提供程序 ID 值。

  例如，如果 Contoso 为 MCC + MNC 值 100 101 提供了四个 APNs，则它会列出电子表格的新行中的每个 APN 条目，并为这四个条目中的每个条目编号从1开始，编号最多为4个条目，因为它们共享相同的 IMSI 范围。 如果 Contoso 为 MCC + MNC 值 100 102 设置了另一组 APNs，则应在该 APNs 集的1处启动自动连接顺序。

  如果未提供自动连接顺序，Windows 会要求用户选择 APN，这可能会导致用户错误。 建议指定自动连接顺序。 在这种情况下，用户会在 Windows 连接管理器中看到该 APN 的 **友好名称** 。

### <a name="apn-database-and-cosa-considerations"></a>APN 数据库和 COSA 注意事项

对于 COSA 和 APN 数据库，请注意以下各项。

- OEM 提供的更改将优先于 Windows 中包含的默认 COSA/APN 数据库。

- 电子表格中的 **国家/地区** 和 **运算符** 条目用于确定此项是对现有 apn 的更新，还是对新接入点的请求进行的更新。 如果 **国家/地区** 和 **操作员** 字段与 APN 数据库中已存在的内容相匹配，则会删除这些条目，并将其替换为你在电子表格中列出的条目。

    >[!NOTE]
    >由于将删除以前的条目，因此，请务必列出 **操作员** 和 **国家/地区** 组合的所有 APNs，包括未更改的 APNs。

    例如，在电子表格的行中输入以下值时：

    ```syntax
     Operator: Contoso
     Country/Region: Argentina
    ```

    COSA 或 APN 连接数据库中当前与以下格式匹配的所有条目将被删除，并将替换为电子表格中对应于该 **操作员** 和 **国家/地区** 组合的行：

    ```syntax
    <Operator name="Contoso (Argentina)">
    ```

-   如果 **操作员** 和 **国家/地区** 条目与 COSA 或 APN 数据库中已存在的内容不匹配，则会创建一个新的 APN。

    例如，如果在电子表格的行中输入以下值：

    ```syntax
    Operator: Contoso
    Country/Region: Argentina
    ```

    如果它在相应的连接数据库中不存在，则会在提交被接受后添加一个新条目，如下所示：

    ```syntax
    <Operator name="Contoso (Argentina)">
    ```

-   在提交的电子表格的每一行上，只需指定下列内容之一：

    -   具有空白 IMSI 范围的 MCC + MNC

    -   具有特定 IMSI 范围的 MCC + MNC

    -   具有特定 ICCID 范围的 MCC + MNC

    -   具有特定 GSM 提供程序名称的 MCC + MNC

-   如果你已经创建了一个用于设置移动宽带服务的网站，则提供帐户体验 URL 和证书数据很重要。

-   用于计划采购 (**采购标志** = **Y**) 的访问字符串可以是以下项之一：

    -   对于 GSM 网络，为用于购买订阅的指定 **用户名** 和 **密码** 的接入点。

    -   对于 CDMA 网络，将使用 (NAI) 的网络访问标识符来购买订阅。

-   用于 Internet 连接 (**连接标志** = **Y**) 的访问字符串可以是以下项之一：

    -   对于 GSM 网络，使用指定 **用户名** 和 **密码** 的 APN 连接到 Internet。

    -   对于 CDMA 网络，将使用 (NAI) 的网络访问标识符连接到 Internet。 

电子表格完成后，可测试已输入的 APNs。 有关测试接入点更新的后续步骤，请参阅 [测试桌面 COSA/APN 数据库提交](testing-your-desktop-cosa-apn-database-submission.md)。

