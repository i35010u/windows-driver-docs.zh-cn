---
title: 规划桌面 COSA/APN 数据库提交
description: 规划桌面 COSA/APN 数据库提交
ms.assetid: 7e974914-c3e5-409e-b0bf-28d6885585b3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adcb656798dfeea1df416e103396140003b76fc0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363086"
---
# <a name="planning-your-desktop-cosaapn-database-submission"></a>规划桌面 COSA/APN 数据库提交

> [!IMPORTANT]
> 从 Windows 10，版本 1703，开始 APN 数据库将替换为新格式称为 COSA。 Windows 8、 Windows 8.1 和 Windows 10 版本 1703年将继续使用 APN 数据库存在时 Windows 10 之前的版本，版本 1703年及更高版本使用 COSA。 有关 COSA 详细信息，请参阅[COSA 概述](cosa-overview.md)。

使用本主题中的部分时想要将新的 APN 添加到基线 COSA/APN 数据库，它随 Windows 桌面设备，或更新现有。

## <a name="the-apn-update-process"></a>APN 更新过程

若要连接到移动宽带网络，用户通常需要提供以下信息：

- GSM 在网络上，如"data.contoso.com"访问点名称 (APN) 是必需的。

- CDMA 网络上访问字符串，其中包含一个特殊拨打代码如"\#777" 或网络访问标识符，例如somebody@contoso.com是必需的。

- 用户名和密码的网络连接。

使用 Windows Update 更新 COSA 和 APN 连接数据库。 下图显示了整个提交过程。

![COSA/APN 数据库提交过程](images/COSA_and_APN_database_submission_process_diagram.png "COSA/APN 数据库提交过程")

## <a name="complete-the-apncosa-update-spreadsheet"></a>完成 APN/COSA 更新电子表格

APN 更新电子表格用于收集所需的信息，以便 Microsoft 能够相应地更新 COSA 或 APN 数据库。 此电子表格包括在向 Microsoft 提交请求。 MOs 应发送给 Microsoft 的所有设备时都目标提交 APN 更新，如果适用的所有信息。

使用以下链接下载最新的 APN 更新电子表格： <https://go.microsoft.com/fwlink/p/?linkid=851213>

有关 APN 更新电子表格中的设置的详细信息，请参阅[桌面 COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

## <a name="considerations-when-completing-the-spreadsheet"></a>完成电子表格时的注意事项

### <a name="apn-database-considerations"></a>APN 数据库注意事项

仅提交为 Windows 8、 Windows 8.1 或 Windows 10 版本 1703年的 Windows 10 之前的版本使用 apndatabase.xml，APN 更新时，请注意以下。

- 运算符标识数据存储在 APN 数据库作为已编码的硬件 Id。
  -   对于 GSM 网络，您可以 MCC/mnc 对每个唯一组合的单独的数据库条目。 如果是移动虚拟网络运算符 (MVNO) 并不具有唯一的 MCC/mnc 对，您可以指定一个或多个范围的 IMSIs 或 SIM ICC Id 当前租用从移动网络运算符 (MNO)。
  -   对于 CDMA 网络，可以为每个提供程序 ID （也称为一个 SID） 或提供程序名称具有新的数据库条目。
  -   帐户预配的元数据的证书信息包括**证书颁发者名称**并**证书使用者名称**并用于验证的帐户预配的采购网站提供来自授权的 web 服务。 如果该证书的信息存储在此处购买网站提供的匹配项，Windows 将允许将特定于网络的配置信息推送到 PC 该网站。

- 提交时使用 apndatabase.xml APN 数据库更新，必须包含以下值：       
    - CDMA 提供程序名称
    - CDMA 提供程序 ID (SID)

- 帐户预配的元数据的证书信息包括**证书颁发者名称**并**证书使用者名称**并用于验证的帐户预配的采购网站提供来自授权的 web 服务。 如果该证书的信息存储在此处购买网站提供的匹配项，Windows 将允许将特定于网络的配置信息推送到 PC 该网站。 

- 自动连接顺序必须是唯一的**运算符**并**国家/地区**配合相同 IMSI，ICCID 范围、 CDMA 提供程序名称或 CDMA 提供程序 ID 值。

  例如，如果 Contoso 有四个 MCC + mnc 值 100 101 APNs，它将列出该电子表格中的新行中每个 APN 条目和编号从 1 开始的最多 4 个四个条目的每个因为它们共享相同的 IMSI 范围的自动连接顺序。 如果 Contoso 有 MCC + mnc 是否值 100 102 APNs 的另一套，它应启动自动连接 1 APNs 该集的排序。

  如果未提供自动连接顺序，Windows 将要求用户选择 APN，这会带来用户错误。 我们建议指定自动连接顺序。 在这种情况下，用户会看到**友好名称**的 APN Windows 连接管理器中。

### <a name="apn-database-and-cosa-considerations"></a>APN 数据库和 COSA 注意事项

请注意以下项作为 COSA 和 APN 数据库。

- OEM 提供的更改将优先于在 Windows 中包含的默认 COSA/APN 数据库。

- **国家/地区**并**运算符**使用电子表格中的条目来确定这是否是对现有 APN 或新 APN 的请求的更新。 如果**国家/地区**并**运算符**字段与 APN 数据库中已存在的内容匹配，将删除条目，并将其替换为您的电子表格中列出的条目。

    >[!NOTE]
    >因为以前的条目将被删除，务必要列出所有的 APNs**运算符**并**国家/地区**组合，包括那些没有做任何更改。

    例如，当输入以下值在电子表格中的行：

    ```syntax
     Operator: Contoso
     Country/Region: Argentina
    ```

    COSA 或 APN 连接中当前的所有条目都数据库将删除以下格式，并将其替换为此，为您的电子表格中的行相匹配**运算符**并**国家/地区**组合：

    ```syntax
    <Operator name="Contoso (Argentina)">
    ```

-   如果**运算符**并**国家/地区**条目与 COSA 或 APN 数据库中已存在的内容不匹配，创建新的 APN。

    例如，如果在电子表格中的行中输入以下值：

    ```syntax
    Operator: Contoso
    Country/Region: Argentina
    ```

    如果它不存在适当的连接数据库中，这看起来像以下接受你的提交后添加新条目：

    ```syntax
    <Operator name="Contoso (Argentina)">
    ```

-   在提交该电子表格的每个行，必须指定只有以下项之一：

    -   MCC + mnc 有空白 IMSI 范围

    -   MCC + mnc 与特定 IMSI 范围

    -   MCC + mnc 与特定的 ICCID 范围

    -   MCC + mnc 具有特定 GSM 提供程序名称

-   如果已创建用于移动宽带服务设置的网站，则务必提供帐户体验 URL 和证书数据。

-   访问用于计划购买的字符串 (**购买标志**=**Y**) 可以是以下之一：

    -   对于 GSM 网络，与指定 APN**用户名**并**密码**用于购买订阅。

    -   对于 CDMA 网络，网络访问标识符 (NAI) 使用购买订阅。

-   访问用于 Internet 连接的字符串 (**连接标志**=**Y**) 可以是以下之一：

    -   对于 GSM 网络，与指定 APN**用户名**并**密码**用于连接到 Internet。

    -   对于 CDMA 网络，网络访问标识符 (NAI) 用于连接到 Internet。 

完成您的电子表格后，你可以测试你输入的 APNs。 下一步骤中测试你的 APN 更新，请参阅[测试您的桌面 COSA/APN 数据库提交](testing-your-desktop-cosa-apn-database-submission.md)。

