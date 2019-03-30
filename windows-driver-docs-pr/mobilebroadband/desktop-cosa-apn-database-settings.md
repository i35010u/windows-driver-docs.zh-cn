---
title: 桌面 COSA/APN 数据库设置
description: 桌面 COSA/APN 数据库设置
ms.assetid: 860B8587-1D70-466A-A6E7-836380AA4DFA
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 35cd4a2c3c52ad09012a316ada8a1da7a35842c1
ms.sourcegitcommit: bb4f9c8dab2f4cb7a57ebd30457f427d909c928f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58624778"
---
# <a name="desktop-cosaapn-database-settings"></a>桌面 COSA/APN 数据库设置

本主题介绍在 desktop COSA 中可用的设置和 APN 数据库 (apndatabase.xml)。

有关桌面 COSA/APN 数据库提交过程的详细信息，请参阅[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。

有关 COSA 的详细信息，请参阅[COSA 概述](cosa-overview.md)。

APN 数据库有关的详细信息，请参阅[APN 数据库概述](apn-database-overview.md)。

## <a name="apn-database-only-settings"></a>APN 仅限于数据库设置

在电子表格中的以下设置适用于仅限 APN 数据库。 如果你面向的 Windows 8、 Windows 8.1 或 Windows 10 版本 1703年的 Windows 10 之前的版本，将使用这些条目。

| 设置名称 | 描述 | 可选或必需 | 说明 |
| --- | --- | --- | --- |
| CDMA ProviderID | 应与你的设备报告 CDMA 提供程序 ID （也称为 SID） 匹配一个 5 位数字。 | 可选 | |
| CDMA ProviderName | 应与你的设备报告 CDMA 提供程序名称匹配的不超过 36 个字符的字符串。 此设置是区分大小写。 | 可选 | |
| CertIssuerName | 用于运算符 XML 设置为签名证书的证书颁发者名称。 | 可选 | 如果指定，还必须指定证书使用者名称和运营商的 GUID。 |
| CertSubjectName | 用于运算符 XML 设置为签名证书的证书使用者名称。 | 可选 | 如果指定，还必须指定证书颁发者名称和运营商的 GUID。 |
| 运营商的 GUID | 是自分配的 GUID 在将来使用运算符 XML 预配包。 | 可选 | 如果指定，还必须指定证书使用者名称和证书颁发者名称。 |
| GSM ProviderName | 一个由你的设备报告的 GSM 提供程序名称应匹配的不超过 36 个字符的字符串。 此设置是区分大小写。 | 可选 | 仅在 Windows 8.1 和 Windows 10 版本 1703年的 Windows 10 之前的版本上支持此设置。 |
| 购买 | 是或否值描述如果预配此 APN 或购买。 | 必需 | 可能值： <ul><li>**Y** – 如果 APN 预配或购买</li><li>**N** – 如果 APN 不是预配或购买</li></ul> <p>如果**采购标志**设置为**Y**，则**连接标志**设置必须为**N**。</p> |
| 连接 | 是或否值描述如果预配此 APN 或购买。 | 必需 | 可能值： <ul><li>**Y** – 如果 APN 预配或购买</li><li>**N** – 如果 APN 不是预配或购买</li></ul> <p>如果**连接标志**设置为**Y**，则**购买标志**设置必须为**N**。</p> |

## <a name="apn-database-and-desktop-cosa-settings"></a>APN 数据库和桌面 COSA 设置

以下各项适用于 APN 数据库和桌面 COSA。 COSA，对于 Windows 所需的最低支持的版本中的最后一列表示。


| 设置名称 | 描述 | 可选或必需 | 说明 | 最小支持 COSA 的 Windows 版本 |
| --- | --- | --- | --- | --- |
| UpdateType | 描述 APN 数据库条目的新的或修改。 | 必需 | 可能值： <ul><li>**添加**– 新的条目</li><li>**更改**– 更新现有条目</li><li>**保留**– 不要更改该条目</li><li>**删除**– 删除的项</li></ul> | Windows 10 版本 1703 |
| 国家/地区 | 国家或地区的 APN 条目。 | 必需 | 此条目可能会更改以匹配 Windows 指在特定国家/地区或区域。 |  Windows 10 版本 1703 |
| 运算符 | 操作员的名称。 不需要此字段中包含的国家或地区。 | 必需 | 请确保使用相同的拼写和大小写的 APN 条目提交更新每个时间。 | Windows 10 版本 1703 |
| MCC | 用于 GSM IMSI 提交一个 3 位 MCC 值。 | 可选的 ICCID 范围。 |  | Windows 10 版本 1703 |
| MNC | 对于 GSM IMSI 提交使用 2 或 3 位 mnc 值。 | 可选的 ICCID 范围。 |  | Windows 10 版本 1703 |
| IMSI 范围-开始 | 包括 MCC + 数开头 mnc 一个 15 位数字。 | 可选 | 数量应以 00 结尾。 <p>如果此设置并**IMSIRange-最终**设置保留为空，但**MCC**和**mnc 是否**指定条目，涵盖整个 MCC + mnc 是否范围。</p> | Windows 10 版本 1703 |
|  IMSI 范围的结束  | 包括 MCC + 数开头 mnc 一个 15 位数字。 | 可选 | 数量应以 99 结尾。 <p>如果此设置并**IMSI 范围的开始**设置保留为空，但**MCC**并**mnc 是否**指定条目，则整个 MCC + mnc 是否所涵盖范围。</p> | Windows 10 版本 1703 |
| ICCID 范围-开始 |  开头 89 （ICCID 颁发者标识符号） 19 或 20 位数字。 | 可选 | 数量应以 00 结尾。  | Windows 10 版本 1703 |
| ICCID 范围的结束  |  开头 89 （ICCID 颁发者标识符号） 19 或 20 位数字。 | 可选 | 数量应以 99 结尾。  | Windows 10 版本 1703 |
| AccountExperienceURL |  如果用户不具有活动的计划，并尝试连接到网络，请使用通过 Windows 连接管理器。  | 可选 | 帮助提高计划的采集体验。 <p>如果**两者**指定了 AppID 和 AccountExperienceURL、 AppID 接收较高的优先级并且将 UX**不**显示 AccountExperienceURL。</p> | Windows 10 版本 1703 |
| FriendlyName | 此 APN 项易于理解且具有意义到订阅服务器的名称。 | 可选 | 将显示在 Windows 连接管理器中，Windows 无法自动连接到网络的情况。 | Windows 10 版本 1703 |
| AccessString | 对于 GSM 网络，这是如 data.contoso.com APN。 对于 CDMA 网络，这是包括如 #777 或网络访问标识符的特殊拨号代码，如访问字符串example@contoso.com。 | 必需 |  | Windows 10 版本 1703 |
| UserName | 用来连接到你的 APN 的用户名称。 此设置是区分大小写。  | 可选 |  | Windows 10 版本 1703 |
| 密码 |  用于连接到你的 APN 的密码。 此设置是区分大小写。  | 可选 |  | Windows 10 版本 1703 |
| AuthProtocol | 指定要用于激活的数据包数据协议 (PDP) 上下文的身份验证协议。 | 可选 | 可能值： <ul><li>**无**– 无身份验证协议是必需的</li><li>**PAP** – PAP 身份验证是必需的。</li><li>**CHAP** – CHAP 身份验证是必需的。</li><li>**MsCHAPV2** -MSCHAPv2 是需要进行身份验证。</li></ul> <p>仅在 Windows 8.1 和 Windows 10 版本 1703年的 Windows 10 之前的版本上支持此设置。</p> | Windows 10 版本 1703 |
| 压缩 | 指定是否将标头和数据传输使用的数据链接压缩。  | 可选 | 可能值： <ul><li>**启用**– 启用压缩</li><li>**禁用**– 未启用压缩</li></ul> <p>仅在 Windows 8.1 和 Windows 10 版本 1703年的 Windows 10 之前的版本上支持此设置。</p> | Windows 10 版本 1703 |
| AutoConnectOrder | Windows 会尝试向 APNs 由操作员提供并标记为"自动连接"APN 数据库或 COSA 中直到其成功连接到移动网络的连接。 如果所有的自动连接尝试失败，Windows 将显示允许用户选取 APN 或输入自定义 APN 的提示。 | 可选 | 如果您有多个访问字符串的运算符来说，此设置必须从 1 开始。 这所需 Windows 尝试共享 IMSI 范围、 ICCID 范围、 CDMA 提供程序 ID 或 CDMA 的多个 APN 条目提供程序名称，当用户尝试连接。 | Windows 10 版本 1809 |

## <a name="desktop-cosa-only-settings"></a>桌面 COSA 限设置

以下设置适用于桌面 COSA 仅。 如果你面向 Windows 10 版本 1703年及更高版本，将使用这些条目。

| 设置名称 | 描述 | 可选或必需 | 说明 | 支持的最低 Windows 版本 |
| --- | --- | --- | --- | --- |
| SupportDataMarketplace | 描述配置文件条目是否支持移动计划的 true/false 字符串。 | 可选 | <p>启用此设置之前, 请确保您的移动运营商是移动计划程序的一部分。</p><p>如果留空，默认为"false。</p> | Windows 10 版本 1703 |
| SPN | 标识符字符串的服务提供程序名称 (SPN) | 可选 | 有助于识别 MO/MVNO 的网络。 如果为空，则默认为空字符串，并且不执行任何操作。 | Windows 10 版本 1703 |
| AlwaysOn | 介绍连接是否始终上。 | 必需 | 如果留空，默认为"true。 | Windows 10 版本 1703 |
| PurposeGroups | 指定连接的目的，由 Guid 表示目的值的以逗号分隔列表的字符串。 | 必需 | 以下用途值有： <ul><li>**Internet**</li><li>**MMS**</li><li>**IMS**</li><li>**SUPL**</li><li>**购买**</li><li>**管理**</li><li>**应用程序**</li><li>**esim 卡预配**</li></ul> <p> 如果留空，默认为"Internet。</p> | Windows 10 版本 1703 |
| | | 可选 | 以下可选目的组值有： <ul><li>**LTE attach** </li></ul> 指定 LTE 附加通过 COSA APN 在于，通常不必要的附加信息通常直接由基础调制解调器的硬件管理。 但是，在其中调制解调器的硬件不具有附加 APN 值 LTE，网络是不能分配到下，用户设备的情况下，MO 可以选择提供 LTE 附加信息，以便 UE 可以 LTE 附加而无需用户手动输入一个值。 | Windows 10，版本 1903 |
| IPType | 一个字符串，指定连接的网络协议。 | 可选 | 可能值： <ul><li>IPv4</li><li>IPv6</li><li>IPv4v6</li></ul> <p>如果留空，默认为"IPv4"。</p> | Windows 10 版本 1703 |
| BrandingName | 移动宽带设备通常提供 Windows Windows 连接管理器中显示的运算符名称。 可以通过在元数据中指定自定义名称来覆盖此名称。 | 可选 | 如果为空，则默认为空字符串，并且不执行任何操作。 | Windows 10 版本 1709 |
| BrandingIcon | 自定义徽标显示在 Windows 连接管理器网络条目旁边。 | 可选 | 图标必须具有透明背景和平滑边缘。 建议测试带有浅色和深色主题的图标。 它们还必须满足以下的格式和大小要求： <ul><li>256 x 256:32 位 + Alpha</li><li>48 x 48:32 位 + Alpha</li><li>48 x 48:8 位 256 色</li><li>48 x 48:4 位 16 种颜色</li><li>32 x 32:32 位 + Alpha</li><li>32 x 32:8 位 256 色</li><li>32 x 32:4 位 16 种颜色</li><li>24 x 24:32 位 + Alpha</li><li>24 x 24:8 位 256 色</li><li>24 x 24:4 位 16 种颜色</li><li>16 x 16:32 位 + Alpha</li><li>16 x 16:8 位 256 色</li><li>16 x 16:4 位 16 种颜色</li></ul> | Windows 10 版本 1709 |
| UseBrandingNameOnRoaming | 确定是否应在漫游或不漫游过程显示品牌。 | 可选 | 可能值： <ul><li>**0** -仅在连接到家庭网络时使用</li><li>**1** -连接到家庭网络和国内漫游时使用</li><li>**2** -连接到家庭网络、 国内漫游和国际漫游时使用</li></ul><p> 如果留空，默认为 0。</p> | Windows 10 版本 1709 |
| Roaming | 指定应在其下激活连接的漫游条件。 | 可选 | 可能值： <ul><li>0:仅在家庭网络</li><li>1：所有漫游的条件 （主页和漫游）</li><li>2：家庭和国内仅漫游</li><li>3：国内仅漫游</li><li>4:非考虑国内盈利仅漫游</li><li>5:仅漫游</li></ul> 如果留空，默认值为 1 （所有漫游条件）。 | Windows 10 版本 1709 |
| DataMarketplaceRoamingUIEnabled | 此设置控制是否应为 SIM 或作为计划移动服务的一部分的 esim 卡显示漫游 UI。 | 可选 | 此设置适用于**SupportDataMarketPlace**设置。 可能的值为： <ul><li>0:将漫游指示器**永远不会**显示。</li><li>1：当设备漫游在外的国家/地区显示漫游的指示器。</li></ul> <p>如果为空，则默认为**1**。</p> | Windows 10 版本 1709 |
| UIName | 如果 （SPN、 MCC、 mnc、 IMSI 范围、 ICCID 范围等） 的目标条件值不能指示唯一项，则 COSA 将显示此名称对最终用户以支持手动选择要使用哪个月连接值。 | 可选 | 例如， **ContosoMVNO**是 MVNO。 它没有任何可用于将自身与主月网络区分开来的唯一值**Contoso**。 在这种情况下， **UIName**可用并且将显示在 Windows 设置 UI 中，使用户可以手动选择预配设置要使用哪个月。 | Windows 10 版本 1709 |
| UIOrder | 控件的索引**UIName**值的下拉列表选取器位置。 | 需要**UIName**指定，则为否则为可选 | 如果未指定，默认值为**0**。 | Windows 10 版本 1709 |
| ESIM_PROV | 描述配置文件是否被视为预配配置文件 esim 卡的 true/false 字符串。 | **重要**可选除非 MO 支持 esim 卡预配配置文件，在这种情况下它是必需。 | <p>如果留空，默认为"false。</p> <p>Esim 卡预配配置文件是一个单一用途配置文件。 EUICC 上安装它时，它使用户的设备来限制的连接到 MO 的围墙花园若要购买的常规、 运营 esim 卡配置文件。</p> | Windows 10 版本 1709 |
| AppID | 描述的包系列名称 (PFN) 和移动运营商的 UWP 辅助应用程序的应用程序 ID 的字符串。 | 可选 | 在 Windows 10，版本 1803年和更高版本， **AppID**用于标识 MOs 具有其辅助应用程序。 **AppID**必须声明为采用以下格式： <p>**PFN!AppId**</p><p>**请注意**此格式是区分大小写。</p><p>若要获取 PFN 和 AppId 为你的应用，请执行以下步骤：<ol><li>获取 PFN 上指定[查看应用程序标识详细信息](https://docs.microsoft.com/windows/uwp/publish/view-app-identity-details)。</li><li>通过打开你的解决方案的查找 AppId *AppManifest.XML*文件和查询 AppXManifest 应用程序 id。</li></ol> <p>有关为 MOs UWP 辅助应用程序的详细信息，请参阅[UWP 移动宽带应用](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/windows-store-mobile-broadband-apps)。</p> | Windows 10 版本 1803 |
| 热点 | 确定是否想要允许用户共享其移动宽带连接用作个人热点。 | 可选 | 可能值： <ul><li>从不</li><li>始终</li><li>EntitlementCheckRequired</li></ul> <p>如果留空，默认为"始终"。</p> <p>*EntitlementCheckRequired*选项使用户能够共享其热点授权检查，这就需要为 Windows 通知事件的处理程序。 如果选择此选项，你需要开发用于处理授权检查请求的月 UWP 配套应用。</p> <p>有关为 MOs UWP 辅助应用程序的详细信息，请参阅[UWP 移动宽带应用](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/windows-store-mobile-broadband-apps)。</p><p>有关 EntitlementCheck API 的详细信息，请参阅其[UWP API 参考页](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.tetheringentitlementchecktriggerdetails)。</p> | Windows 10 版本 1803 |
