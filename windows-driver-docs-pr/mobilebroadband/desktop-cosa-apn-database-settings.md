---
title: 桌面 COSA/APN 数据库设置
description: 桌面 COSA/APN 数据库设置
ms.assetid: 860B8587-1D70-466A-A6E7-836380AA4DFA
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 35cd4a2c3c52ad09012a316ada8a1da7a35842c1
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79243012"
---
# <a name="desktop-cosaapn-database-settings"></a>桌面 COSA/APN 数据库设置

本主题介绍桌面 COSA 和 APN 数据库（apndatabase）中的可用设置。

有关桌面 COSA/APN 数据库提交过程的详细信息，请参阅[计划桌面 COSA/apn 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。

有关 COSA 的详细信息，请参阅[COSA 概述](cosa-overview.md)。

有关 APN 数据库的详细信息，请参阅[apn 数据库概述](apn-database-overview.md)。

## <a name="apn-database-only-settings"></a>APN 仅限数据库设置

电子表格中的以下设置仅适用于 APN 数据库。 如果面向 windows 8、Windows 8.1 或 windows 10 版本1703之前的版本，则将使用这些项。

| 设置名称 | 说明 | 可选或必需 | 注意 |
| --- | --- | --- | --- |
| CDMA ProviderID | 与设备报告的 CDMA 提供程序 ID （也称为 SID）匹配的5位数字。 | 可选 | |
| CDMA ProviderName | 不超过36个字符的字符串，该字符串应与设备报告的 CDMA 提供程序名称匹配。 此设置区分大小写。 | 可选 | |
| CertIssuerName | 用于操作员 XML 预配的签名证书的证书颁发者名称。 | 可选 | 如果已指定，则还必须指定证书使用者名称和运营商 GUID。 |
| CertSubjectName | 用于操作员 XML 预配的签名证书的证书使用者名称。 | 可选 | 如果已指定，则还必须指定证书颁发者名称和运营商 GUID。 |
| 电信公司 GUID | 在未来的 operator XML 预配包中使用的自分配 GUID。 | 可选 | 如果已指定，则还必须指定证书使用者名称和证书颁发者名称。 |
| GSM ProviderName | 不超过36个字符的字符串，该字符串应与设备报告的 GSM 提供程序名称匹配。 此设置区分大小写。 | 可选 | 此设置仅支持 windows 10 版本1703之前的 Windows 10 Windows 8.1 和版本。 |
| 购买 | "是" 或 "否" 值，用于描述 APN 是否正在预配或购买。 | 必需 | 可能的值： <ul><li>**Y** -如果 APN 正在预配或购买</li><li>**N** –如果未预配或购买 APN</li></ul> <p>如果**购买标志**设置为**Y**，则**连接标志**设置必须为**N**。</p> |
| 连接 | "是" 或 "否" 值，用于描述 APN 是否正在预配或购买。 | 必需 | 可能的值： <ul><li>**Y** -如果 APN 正在预配或购买</li><li>**N** –如果未预配或购买 APN</li></ul> <p>如果**连接标志**设置为**Y**，则**采购标志**设置必须为**N**。</p> |

## <a name="apn-database-and-desktop-cosa-settings"></a>APN 数据库和 desktop COSA 设置

以下条目适用于 APN 数据库和桌面 COSA。 对于 COSA，最后一列指出了所需的最小 Windows 版本。


| 设置名称 | 说明 | 可选或必需 | 注意 | COSA 支持的最低 Windows 版本 |
| --- | --- | --- | --- | --- |
| UpdateType | 描述 APN 数据库条目是新增还是修改。 | 必需 | 可能的值： <ul><li>**添加**–新条目</li><li>**更改**–更新现有条目</li><li>**保留**-不更改条目</li><li>**删除**–删除条目</li></ul> | Windows 10 版本 1703 |
| 国家（地区）/区域 | APN 条目的国家或地区。 | 必需 | 此项可能会更改以匹配 Windows 如何引用特定的国家或地区。 |  Windows 10 版本 1703 |
| 运算符 | 操作员的名称。 不需要在此字段中包含国家或地区。 | 必需 | 确保每次提交 APN 项的更新时均使用相同的拼写和大小写。 | Windows 10 版本 1703 |
| MCC | 用于 GSM IMSI 报送的3位数 MCC 值。 | 对于 ICCID 范围是可选的。 |  | Windows 10 版本 1703 |
| MNC | 用于 GSM IMSI 报送的2位数或3位 MNC 值。 | 对于 ICCID 范围是可选的。 |  | Windows 10 版本 1703 |
| IMSI 范围-开始 | 一个包含数字开头的 MCC + MNC 的15位数字。 | 可选 | 该数字应以00结束。 <p>如果此设置和 " **IMSIRange** " 设置为空，但指定了**mcc**和**MNC**条目，则会涵盖整个 MCC + MNC 范围。</p> | Windows 10 版本 1703 |
|  IMSI 范围-结束  | 一个包含数字开头的 MCC + MNC 的15位数字。 | 可选 | 该数字应以99结束。 <p>如果此设置和 " **IMSI 范围-启动**" 设置留空，但指定了**mcc**和**MNC**条目，则会涵盖整个 MCC + MNC 范围。</p> | Windows 10 版本 1703 |
| ICCID 范围-开始 |  以89（ICCID 颁发者标识符号）开头的19或20位数字。 | 可选 | 该数字应以00结束。  | Windows 10 版本 1703 |
| ICCID 范围-结束  |  以89（ICCID 颁发者标识符号）开头的19或20位数字。 | 可选 | 该数字应以99结束。  | Windows 10 版本 1703 |
| AccountExperienceURL |  如果用户没有活动计划并尝试连接到网络，则由 Windows 连接管理器使用。  | 可选 | 有助于改进计划获取体验。 <p>如果**同时**指定了 Appid 和 AccountExperienceURL，appid 会获得更高的优先级，并且 UX**不**会显示 AccountExperienceURL。</p> | Windows 10 版本 1703 |
| FriendlyName | 此 APN 项的名称，该名称可理解并对订阅者有用。 | 可选 | 在 windows 无法自动连接到网络的情况下出现在 Windows 连接管理器中。 | Windows 10 版本 1703 |
| AccessString | 对于 GSM 网络，这是一个接入点，例如 data.contoso.com。 对于 CDMA 网络，此访问字符串包含特殊的拨号代码，如 #777 或网络访问标识符，如 example@contoso.com。 | 必需 |  | Windows 10 版本 1703 |
| UserName | 用于连接到 APN 的用户名。 此设置区分大小写。  | 可选 |  | Windows 10 版本 1703 |
| 密码 |  用于连接到 APN 的密码。 此设置区分大小写。  | 可选 |  | Windows 10 版本 1703 |
| AuthProtocol | 指定用于激活数据包数据协议（PDP）上下文的身份验证协议。 | 可选 | 可能的值： <ul><li>**无**-无需身份验证协议</li><li>**Pap** –要求执行 pap 身份验证。</li><li>需要**chap** -chap 身份验证。</li><li>**Eap-mschapv2** –需要进行身份验证。</li></ul> <p>此设置仅支持 windows 10 版本1703之前的 Windows 10 Windows 8.1 和版本。</p> | Windows 10 版本 1703 |
| 压缩 | 指定是否在数据链路上使用压缩来标头和数据传输。  | 可选 | 可能的值： <ul><li>**启用**–启用压缩</li><li>**禁用**–不启用压缩</li></ul> <p>此设置仅支持 windows 10 版本1703之前的 Windows 10 Windows 8.1 和版本。</p> | Windows 10 版本 1703 |
| AutoConnectOrder | Windows 尝试连接到操作员提供的 APNs 并在 APN 数据库或 COSA 中标记为 "自动连接"，直到成功连接到移动网络。 如果所有自动连接尝试均失败，则 Windows 将显示一条提示，允许用户选择 APN 或输入自定义接入点。 | 可选 | 如果一个操作员有多个访问字符串，则此设置必须以1开头。 当用户尝试连接时，Windows 将尝试使用多个共享 IMSI 范围、ICCID 范围、CDMA 提供程序 ID 或 CDMA 提供程序名称的 APN 条目。 | Windows 10 版本 1809 |

## <a name="desktop-cosa-only-settings"></a>仅桌面 COSA 设置

以下设置仅适用于桌面 COSA。 如果你面向的是 Windows 10 版本1703及更高版本，则将使用这些项。

| 设置名称 | 说明 | 可选或必需 | 注意 | 支持的最低 Windows 版本 |
| --- | --- | --- | --- | --- |
| SupportDataMarketplace | 描述配置文件项是否支持移动计划的 true/false 字符串。 | 可选 | <p>在启用此设置之前，请确保移动运营商是移动计划计划的一部分。</p><p>如果留空，默认值为 "false"。</p> | Windows 10 版本 1703 |
| SPN | 服务提供程序名称（SPN）的标识符字符串 | 可选 | 有助于识别 MO/MVNO 的网络。 如果留空，则默认为空字符串，并且不执行任何操作。 | Windows 10 版本 1703 |
| AlwaysOn | 描述连接是否始终打开。 | 必需 | 如果留空，默认值为 "true"。 | Windows 10 版本 1703 |
| PurposeGroups | 一个字符串，该字符串通过以逗号分隔的表示目的值的 Guid 列表指定连接目的。 | 必需 | 可用值如下： <ul><li>**互联**</li><li>**彩信**</li><li>**IMS**</li><li>**SUPL**</li><li>**购买**</li><li>**公用**</li><li>**应用程序**</li><li>**eSIM 预配**</li></ul> <p> 如果留空，默认值为 "Internet"。</p> | Windows 10 版本 1703 |
| | | 可选 | 以下可选的用途组值可用： <ul><li>**LTE 附加** </li></ul> 通常不需要通过 COSA 指定 LTE 附加 APN，因为附加信息通常由基础调制解调器的硬件直接管理。 但是，在调制解调器的硬件没有 LTE 附加 APN 值并且网络不能将其分配给 UE 时，MO 可以选择提供 LTE 附加信息，以便 UE 无需用户手动输入值即可连接到连接。 | Windows 10 版本 1903 |
| IPType | 一个字符串，指定连接的网络协议。 | 可选 | 可能的值： <ul><li>IPv4</li><li>IPv6</li><li>IPv4v6</li></ul> <p>如果留空，默认值为 "IPv4"。</p> | Windows 10 版本 1703 |
| BrandingName | 移动宽带设备通常提供操作员名称，Windows 连接管理器中会显示该名称。 可以通过在元数据中指定自定义名称来覆盖此名称。 | 可选 | 如果留空，则默认为空字符串，并且不执行任何操作。 | Windows 10 版本 1709 |
| BrandingIcon | 出现在网络项旁边的 Windows 连接管理器中的自定义徽标。 | 可选 | 图标必须具有透明背景和平滑边缘。 建议使用浅色和深色主题测试图标。 它们还必须满足以下格式和大小要求： <ul><li>256 x 256：32位 + Alpha</li><li>48 x 48：32位 + Alpha</li><li>48 x 48：8位 256 color</li><li>48 x 48：4位16色</li><li>32 x 32：32位 + Alpha</li><li>32 x 32：8位 256 color</li><li>32 x 32：4位16色</li><li>24 x 24:32 位 + Alpha</li><li>24 x 24: 8 位256颜色</li><li>24 x 24: 4 位16色</li><li>16 x 16:32 位 + Alpha</li><li>16 x 16: 8 位256色</li><li>16 x 16: 4 位16色</li></ul> | Windows 10 版本 1709 |
| UseBrandingNameOnRoaming | 确定是否应在漫游或不漫游期间显示品牌。 | 可选 | 可能的值： <ul><li>**0** -仅在连接到家庭网络时使用</li><li>**1** -连接到家庭网络和国内漫游时使用</li><li>**2** -连接到家庭网络、国内漫游和国际漫游时使用</li></ul><p> 如果留空，默认值为0。</p> | Windows 10 版本 1709 |
| Roaming | 指定应在其下激活连接的漫游条件。 | 可选 | 可能的值： <ul><li>0：仅限家庭网络</li><li>1：所有漫游条件（home 和漫游）</li><li>2：仅限家庭和国内漫游</li><li>3：仅限国内漫游</li><li>4：仅限非国内漫游</li><li>5：仅漫游</li></ul> 如果留空，默认值为1（所有漫游条件）。 | Windows 10 版本 1709 |
| DataMarketplaceRoamingUIEnabled | 此设置控制是否应显示属于移动计划服务一部分的 SIM 或 eSIM 的漫游用户界面。 | 可选 | 此设置适用于**SupportDataMarketPlace**设置。 可能的值为： <ul><li>0：**永远不**会显示漫游指示器。</li><li>1：当设备漫游到外国国家/地区时，会显示漫游指示器。</li></ul> <p>如果留空，默认值为**1**。</p> | Windows 10 版本 1709 |
| UIName | 如果目标条件值（SPN、MCC、MNC、IMSI 范围、ICCID 范围等）无法指示唯一条目，则 COSA 会将此名称显示给最终用户，以启用手动选择要使用的 MO 连接值。 | 可选 | 例如， **ContosoMVNO**为 MVNO。 它没有任何唯一值可以用于将自身与主 MO 网络**Contoso**区分开来。 在这种情况下，可以使用**UIName**并将在 WINDOWS 设置 UI 中显示，使用户能够手动选择要使用的 MO 设置设置。 | Windows 10 版本 1709 |
| UIOrder | 用于控制**UIName**值的下拉列表选取器位置的索引。 | 如果指定了**UIName** ，则为必需;可选，否则 | 如果未指定，则默认为**0**。 | Windows 10 版本 1709 |
| ESIM_PROV | 描述配置文件是否被视为 eSIM 预配配置文件的 true/false 字符串。 | **重要提示**可选，除非 MO 支持 eSIM 预配配置文件，在这种情况下，它是必需的。 | <p>如果留空，默认值为 "false"。</p> <p>ESIM 预配配置文件是单一用途的配置文件。 当它安装在 eUICC 上时，它使用户的设备能够与 MO 的围墙园建立有限的连接，以便购买常规的操作 eSIM 配置文件。</p> | Windows 10 版本 1709 |
| AppID | 描述移动运营商的 UWP 辅助应用的包系列名称（PFN）和应用程序 ID 的字符串。 | 可选 | 在 Windows 10 中，版本1803和更高版本中， **AppID**用于标识 MOs 及其配套应用。 必须采用以下格式声明**AppID** ： <p>**PFN!AppId**</p><p>**注意**此格式区分大小写。</p><p>若要获取应用的 PFN 和 AppId，请遵循以下步骤：<ol><li>获取[查看应用标识详细信息](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)中指定的 PFN。</li><li>通过打开解决方案的*AppManifest*文件，并查询 appxmanifest.xml 的应用程序 ID 来查找 AppId。</li></ol> <p>有关适用于 MOs 的 UWP 辅助应用的详细信息，请参阅[uwp mobile 宽带应用](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/windows-store-mobile-broadband-apps)。</p> | Windows 10 版本 1803 |
| 热点 | 确定是否允许用户将其移动宽带连接作为个人热点共享。 | 可选 | 可能的值： <ul><li>从不</li><li>始终</li><li>EntitlementCheckRequired</li></ul> <p>如果留空，默认值为 "始终"。</p> <p>使用*EntitlementCheckRequired*选项，用户可以与要求 Windows 通知事件处理程序的权限检查共享其热点。 如果选择此选项，则需要开发一个 MO UWP 辅助应用来处理权限检查请求。</p> <p>有关适用于 MOs 的 UWP 辅助应用的详细信息，请参阅[uwp mobile 宽带应用](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/windows-store-mobile-broadband-apps)。</p><p>有关 EntitlementCheck API 的详细信息，请参阅其[UWP api 参考页](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.tetheringentitlementchecktriggerdetails)。</p> | Windows 10 版本 1803 |
