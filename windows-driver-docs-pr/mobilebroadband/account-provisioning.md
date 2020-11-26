---
title: 帐户预配
description: 帐户预配
ms.assetid: 3ffcd769-253f-4918-8095-a9206445a201
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d90c86107bbd3d55964e841406dcceac33bf0e
ms.sourcegitcommit: 0c3cab853b0b75149b7604eef03275f997792a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96157343"
---
# <a name="account-provisioning"></a>帐户预配

设置是指使用连接到操作员网络所需的信息来配置 Windows 计算机。 预配通常在移动宽带订阅购买后执行。 Windows 从操作员接受基于 XML 的预配文件。 预配 API 通过使用移动宽带应用或通过购买网站来应用操作员提供的预配 XML 文件。

下图说明了预配 XML 文件的内容和层次结构。

![预配 xml 文件层次结构](images/mb-provisioningmetadata.jpg)

有关预配架构的详细信息，请参阅 [CarrierControlSchema 架构](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/schema-root)。

## <a name="updating-the-provisioning-metadata"></a>更新设置元数据

可以通过多种方式来更新计算机上的设置元数据。

### <a name="mobile-broadband-app"></a>移动宽带应用

在计算机上安装移动宽带应用后，它可以根据你在应用中实现的任何触发器来检索或生成更新的预配文件。

移动宽带应用可以使用 [**NetworkOperator. ProvisioningAgent**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent) api 应用设置文件。 如果应用与网络帐户 ID 相关联，则可以使用 [**CreateFromNetworkAccountId**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent#Windows_Networking_NetworkOperators_ProvisioningAgent_CreateFromNetworkAccountId_System_String_) 来提供未签名的元数据。 如果应用没有与网络帐户 ID 相关联，则它必须使用 **ProvisioningAgent** 的默认构造函数，并对 XML 进行签名。

移动宽带应用可以使用以下触发器来更新预配元数据：

- **使用情况** 最初配置数据限制后，可以告知 Windows 每5% 的使用率增量通知应用。 这可确保应用检索最新使用情况信息。

- **计时器** 计时器可以在适当的时间间隔内更新设置元数据。

- **传入短信** 您可以发送您的应用程序理解的 SMS 消息。 这可能会定义启动刷新的消息，或自动检查收到阈值通知时的更新使用情况。

- **Windows 通知服务** 任何 UWP 应用都可以注册推送通知，并根据其内容采取措施。 可以将此作为设置更新的通知通道。

- **大型位置更改** 如果其他参数适用于处于不同区域设置的用户，则位置更改可能会触发应用程序，以便对用户的新位置应用更新的设置。

- **时区更改** 对于大型区域大小，可以将系统时区更改用作位置更改的代理。 对于没有 GPS 或移动宽带的计算机，这可能特别感兴趣。

### <a name="web-based-provisioning"></a>基于 Web 的设置

网站可以使用 [**msProvisionNetworks**](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85)) API 提供设置数据。 必须使用 x.509 证书和 DSig 证书对提供给此 API 的预配文件进行签名。

可以通过使用 APN 数据库、服务元数据或以前的帐户预配元数据文件，将证书预先提供给计算机。 如果证书已受信任，则没有用户交互。 如果计算机以前不知道该证书，则该证书必须是 EV 证书，并在接受该证书之前提示用户同意。

### <a name="automatic-provisioning-refresh"></a>自动设置刷新

预配文件可包含 Windows 的指令，以在计划的时间间隔或响应特定的短信自动检索更新的预配文件。 此方法不要求在本地计算机上安装移动宽带应用。

## <a name="provisioning-metadata-contents"></a>预配元数据内容

预配元数据包括以下部分：

- [全球](#global)

- [启动](#activation)

- [移动宽带信息](#mobile-broadband-information)

- [Wi-fi 信息](#wi-fi-information)

- [计划信息](#plan-information)

- [刷新](#refresh)

- [信号](#signature)

- [允许的组合](#permitted-combinations)

有关这些部分的详细信息，请参阅 [CarrierControlSchema 架构](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/schema-root)。

### <a name="global"></a>全球

每个设置文件中都需要全局部分。 本节中所需的元素如下所示：

- [**CarrierId**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-carrierid) 一个 GUID，用于唯一标识创作文件的组织。 如果要生成移动宽带应用，则必须使用在服务元数据包中 **ServiceInfo.xml** 的 "[服务编号](../dashboard/index.yml)" 字段中指定的 GUID。 有关服务元数据包架构的信息，请参阅 [服务元数据包架构参考](mobilebroadbandinfo-xml-schema.md)。

  > [!NOTE]
  > 这与你在 Windows 开发人员中心仪表板–硬件上 **创建移动宽带体验向导** 中提供的服务编号相同。
  > 如果你不创建移动宽带应用，则可以为组织使用生成 GUID。 无论是哪种情况，都应始终对组织颁发的所有预配文件使用相同的 GUID。

- [**SubscriberId**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-subscriberid) 一个字符串，用于唯一标识组织中的客户。 如果你是移动运营商，这应该是 GSM 操作员的 IMSI 或 ICCID 范围，或 CDMA 运算符的提供程序 ID 或提供程序名称。 如果您不是移动运营商，则可以选择任何足够的唯一字符串。

### <a name="activation"></a>激活

后端上的激活过程完成后，将发生设备激活。 在连接到网络之前，电脑可能需要按照某些说明进行操作。 预配引擎使用设备激活元素中收到的激活说明。 如果未指定任何值，则不需要任何客户端操作。 可用的操作包括：

- **重新连接** 断开连接并连接到操作员网络。

    **重新注册** 断开连接并注册到操作员网络。

- **数据** 要发送到设备以激活连接的数据或说明。 预配引擎将此数据按原样传递到设备。 对于 CDMA，这可能包括说明 **\* 228** 的说明，以启动 OTA 编程会话并重新连接到网络。

### <a name="mobile-broadband-information"></a>移动宽带信息

移动宽带信息包含多个元素：

[**MBNProfiles**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-mbnprofiles)

定义有关移动运营商网络的订阅者信息。 可以使用两个不同的配置文件：

- [**PurchaseProfile**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-purchaseprofile)：连接到操作员的网络以购买新订阅所需的信息。

- [**DefaultProfile**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-defaultprofile) 每个移动宽带订阅可以有一个用于连接到家庭网络操作员的默认配置文件。 Windows 连接管理器使用此配置文件自动连接到网络。

    ```xml
    <MBNProfiles>
        <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
          <Name>Contoso MBN</Name>
          <Description>Contoso Mobile Broadband</Description>
          <HomeProviderName>Contoso MBN</HomeProviderName>
          <Context>
            <AccessString>contoso.com</AccessString>
            <UserLogonCred>
              <UserName>mbuser</UserName>
              <Password>[PLACEHOLDER]</Password>
            </UserLogonCred>
          </Context>
        </DefaultProfile>
      </MBNProfiles>
    ```

[**品牌打造**](/uwp/schemas/mobilebroadbandschema/wwan/element-branding)

> [!IMPORTANT]
> 从 Windows 10 版本1709开始，ProvisioningAgent API 预配的品牌字段已替换为 COSA 数据库中的署名字段。 **徽标** 已替换为 COSA 中的 **品牌图标** ， **名称** 已替换为 COSA 中的 **品牌名称** 。
>
> 在 Windows 10 版本1709及更高版本中进行设置时，将不再考虑 **徽标** 和 **名称**。 如果使用 ProvisioningAgent API，则它不会引发错误，但应改为在 COSA 中更改 **品牌图标** 和 **品牌名称** 。  
>
> 有关 **品牌图标** 和 **品牌名称** 的详细信息，请参阅 [desktop COSA/APN 数据库设置 (桌面 COSA 仅) 设置](desktop-cosa-apn-database-settings.md#desktop-cosa-only-settings)。

署名允许指定 Windows 显示移动宽带网络的方式。 此信息将覆盖任何服务元数据（如果存在）。 如果未提供任何信息，则使用服务元数据包的内容。 品牌元素如下所示：

- [**徽标**](/uwp/schemas/mobilebroadbandschema/wwan/element-logo) Base64 编码的。PNG or.BMP 嵌入在 XML 中的文件。 此徽标适用于你的移动宽带配置文件，可在网络列表中显示。

- [**名称**](/uwp/schemas/mobilebroadbandschema/wwan/element-name) 设置移动宽带配置文件的载波显示名称。

#### <a name="sms-parsing"></a>SMS 分析

您可以预配规则来标识文本消息，并将信息提取为预配 XML 文件的一部分。 您可以使用 SMS 消息来更新数据使用统计信息，或启动设置信息的刷新。 可以通过以下方式来标识这些消息：

- USSD) 的持有者类型 (

- 发件人仅 (短信) 

- 正则表达式

有关 SMS 通知的详细信息，请参阅 [启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

每个规则都包含以下信息：

- **无提示** 如果此值为 true，则消息仅生成 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件。 如果此值为 false，则该消息将生成 **SmsMessageReceived** 事件。

- **允许的发送方** 指定允许通知到达的保留发送方地址。 此数字必须与 SMS 消息中收到的发送方号码完全匹配，包括国际格式。

- **模式** 用于标识并选择性地从文本消息中提取数据字段的正则表达式。 此模式将与发件人的所有消息匹配： `[^]*`

- **RuleId** 此规则的标识符，该标识符将作为 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件的一部分传递到移动宽带应用。 此标识符使应用能够知道哪个规则导致 SMS 触发 MobileOperatorNotification 事件，并可以减少应用再次分析消息的需要。

- **字段和组** 正则表达式模式中的每个捕获组都绑定到一个命名字段。 这用于提取数据并将其转换为一组可用值。 例如，第一个匹配组可以绑定到 **使用情况** 字段，第二个匹配组可以绑定到 **UsageDataLimit** 字段。 此关联指示第一个值是当前使用情况信息，第二个值是允许的最大使用量。

  - **使用情况、UsagePercentage、UsageOverage、UsageOveragePercentage**：以数据上限的百分比形式表示当前使用量，以超出数据限制的数字或超出数据限制的百分比表示。 绝对值可以引用指定值表示单位的组。

  - **UsageTimestamp**：计算用量字段的日期和时间。 如果包括任何 **使用情况 \\** _ 字段，则必须包括此信息。 格式字符串包含以下标识符，以表达应如何解释子字符串：

    |标识符|说明|
    |----|----|
    |% d|以十进制数表示的月内日期 (01 – 31)|
    |% H|24 小时制的小时 (00 – 23)|
    |% I|12 小时制的小时 (01 – 12)|
    |% m|以十进制数表示的月份 (01 – 12)|
    |% M|以十进制数表示的分钟 (00 – 59)|
    |% S|以十进制数表示的秒 (00 – 59)|
    |% y|以十进制数字表示的不带世纪数的年份 (00 – 99)|
    |% Y|Year （带有世纪），小数位数为 (0000-9999) |
    |% p|AM/PM 指示符|
    |% #d，% #H，% #I，% #m，% #M，% #S，% #y，% #Y|与上面相同，但没有前导零|

  - _ * DataLimit * *：允许用户使用的绝对字节数;这包括指定表示值的单位的组。

  - **OverDataLimit，拥塞**：修改报告给应用的标志，以指示用户已超出其数据限制或网络负载过高。

  - **InboundBandwidth，OutboundBandwidth**：如果网络施加了最大带宽，则指定代表值和单位的组。

  - **PlanType**：指定如何向用户收费以供将来使用。

**警告**  
由于 SMS 消息会影响 Windows 行为，因此只能使用受信任的 SMS 消息。 通过限制发送方地址来维护安全性。 此安全方法假设你的网络的 SMS 网关可确保来自受限制发送方的消息不会被欺骗。

### <a name="wi-fi-information"></a>Wi-Fi 信息

本部分允许你为 Windows 提供任意数量的 Wi-Fi 网络配置文件。 部分的格式类似于 Windows native WLAN API 使用的 XML 架构。

> [!NOTE]
> 一个配置文件可以包含多个 Ssid，如果所有其他设置相同。 如果不同的网络)  (身份验证方法、加密设置、计划等不同的方式，则必须创建其他配置文件。

指定 WLAN 部分时，还必须指定要在计算机上配置的所有配置文件。 如果这些配置文件引用数据计划，则还必须包含 "计划" 部分。 处理此部分时发生的行为如下所示：

- 如果计算机具有不再指定的配置文件，则会删除该配置文件。

- 如果指定配置文件，则将更新或创建该配置文件。

- 空的 WLAN 部分会删除所有配置文件。

- 省略 WLAN 部分会使计算机上的 WLAN 配置文件保持不变。

此部分中的其他节点是关联的计划。 此节点使 Windows 能够将 WLAN 配置文件与计划部分中描述的计划相关联。 利用此计划，您可以在计算机连接到网络时通知 Windows 计量状态，并影响 Windows 的行为。

#### <a name="unencrypted-network-no-automatic-authentication"></a>未加密的网络，无自动身份验证

此配置文件将 Windows 配置为连接到打开的网络。

- 如果此网络包含一个捕获的门户，则会在连接到网络时打开浏览器。

- 如果网络不包含固定门户，则用户无需执行任何其他操作即可连接。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
    </security>
  </MSM>
</WLANProfile>
```

#### <a name="unencrypted-network-wispr-authentication"></a>未加密网络，WISPr 身份验证

此配置文件将 Windows 配置为连接到开放网络，并使用无线 Internet 服务提供商漫游 (WISPr) 身份验证：

- 如果网络包含支持 WISPr 的捕获门户，则将指定的用户名和密码提交到指定的身份验证服务器。

- 如果捕获的门户不能进行 WISPr，则会在连接到网络时打开浏览器。

- 如果网络不包含固定门户，则用户无需执行任何其他操作即可连接。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
        <UserName>WisprUser1</UserName>
        <Password>[PLACEHOLDER]</Password>
        <TrustedDomains>
          <TrustedDomain>www.contosoportal.com</TrustedDomain>
        </TrustedDomains>
      </HotspotProfile>
    </security>
  </MSM>
</WLANProfile>
```

#### <a name="encrypted-network-eap-sim-authentication"></a>加密网络，EAP-SIM 身份验证

此配置文件将 Windows 配置为使用 SIM 作为身份验证类型（如热点2.0 网络）连接到加密网络。 热点2.0 将此类网络定义为使用带有 EAP-SIM 身份验证 WPA2-Enterprise。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso Wi-Fi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>WPA2</authentication>
        <encryption>AES</encryption>
        <useOneX>true</useOneX>
      </authEncryption>
      <OneX xmlns="http://www.microsoft.com/networking/OneX/v1">
        <EAcomputeronfig>
          <!-- The config XML for all EA methods can be found at: https://msdn.microsoft.com/library/cc232996(v=prot.10).aspx -->
          <EapHostConfig xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
            <EapMethod>
              <Type>18</Type>
              <VendorId>0</VendorId>
              <VendorType>0</VendorType>
              <AuthorId>311</AuthorId>
            </EapMethod>
            <Config xmlns="http://www.microsoft.com/provisioning/EapHostConfig">
              <EapSim xmlns="http://www.microsoft.com/provisioning/EapSimConnectionPropertiesV1">
                <Realm Enabled="true"></Realm>
              </EapSim>
            </Config>
          </EapHostConfig>
        </EAcomputeronfig>
      </OneX>
    </security>
  </MSM>
</WLANProfile>
```

#### <a name="unencrypted-network-app-based-authentication"></a>未加密的网络，基于应用的身份验证

此配置文件会将 Windows 配置为连接到开放网络，并在你的移动宽带应用程序中结合使用 WISPr 身份验证。

- 如果网络包含一个捕获的门户，你的应用程序将在后台打开以提供 WISPr 凭据。 然后，凭据将提交到指定的身份验证服务器。

- 如果捕获的门户不能进行 WISPr，则会在连接到网络时打开浏览器。

- 如果网络不包含固定门户，则用户无需执行任何其他操作即可连接。

``` syntax
<WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
  <name>Contoso WiFi</name>
  <SSIDConfig>
    <SSID>
      <name>Contoso Wi-Fi</name>
    </SSID>
  </SSIDConfig>
  <MSM>
    <security>
      <authEncryption>
        <authentication>open</authentication>
        <encryption>none</encryption>
        <useOneX>false</useOneX>
      </authEncryption>
      <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
        <ExtAuth>
          <ExtensionId>YourAppIdGoesHere</ExtensionId>
        </ExtAuth>
        <TrustedDomains>
          <TrustedDomain>www.contosoportal.com</TrustedDomain>
        </TrustedDomains>
      </HotspotProfile>
    </security>
  </MSM>
</WLANProfile>
```

### <a name="plan-information"></a>计划信息

每个移动宽带和热点配置文件都引用一个计划。 多个配置文件可引用同一计划。 在单独的顶级部分介绍了计划。

计划分为两部分：*说明* 和 *使用情况*。 这样，你就可以在较大的预配文件中最初提供配置文件和说明，然后提供较小的预配文件，其中仅包含客户的当前使用情况。

此信息用于直接影响 Windows 的行为，并提供给应用程序，以便为网络自适应其行为。 此信息可通过网络信息 Api 提供给第三方应用程序。

### <a name="description"></a>说明

通常在客户的订阅期间使用低频率更改的元素，包括：

- [**PlanType**](/uwp/schemas/mobilebroadbandschema/wwan/element-plantype) 客户与操作员的计费关系类型：

  - **无限制** 使用不会产生额外的费用。

  - 已 **修复** 为用户分配了一定量的固定成本。

  - **变量** 用户根据使用情况付费。

- [**SecurityUpdatesExempt**](/uwp/schemas/mobilebroadbandschema/plans/element-securityupdatesexempt) 指定安全更新是否计入客户使用情况的布尔值。

- [**DataLimitInMegabytes**](/uwp/schemas/mobilebroadbandschema/plans/element-datalimitinmegabytes) 如果 [**PlanType**](/uwp/schemas/mobilebroadbandschema/wwan/element-plantype) 是 **固定** 的，则为用户分配的使用情况。

- [**BillingCycle**](/uwp/schemas/mobilebroadbandschema/plans/element-billingcycle) 定义计划的开始日期和时间、持续时间和计费周期结束后发生的情况。

- [**BandwidthInKbps**](/uwp/schemas/mobilebroadbandschema/dusm/element-bandwidthinkbps) 网络允许的用户连接速度;这可以反映其计划的标准，或反映由于拥塞或过度使用 (最大为 2 Gbps) 而导致载波当前所强加的比率。

- [**MaxTransferSizeInMegabytes**](/uwp/schemas/mobilebroadbandschema/plans/element-maxtransfersizeinmegabytes) 一个整数，表示符合应用程序应该允许通过按流量计费的连接的单个下载大小，而无需明确地用户批准所使用的连接。

- [**UserSMSEnabled**](/uwp/schemas/mobilebroadbandschema/plans/element-usersmsenabled) 指示计划是否包括用户到用户的 SMS 支持。 如果为 true，则即使未使用移动宽带接口，Windows 也会将连接到网络的设备保持连接备用状态。 如果为 false，则 Windows 可以关闭移动宽带接口的电源，以节省电源，从而导致设备在计算机空闲时无法通过网络进行寻址。

### <a name="usage"></a>使用情况

以下元素可以更改为更高的频率：

- [**UsageInMegabytes**](/uwp/schemas/mobilebroadbandschema/dusm/element-usageinmegabytes) 用户最近的数据使用情况。

- [**OverDataLimit**](/uwp/schemas/mobilebroadbandschema/wwan/element-overdatalimit) 一个布尔值，如果 [**PlanType**](/uwp/schemas/mobilebroadbandschema/wwan/element-plantype) 是 **固定** 的，则指示用户是否已通过分配的使用情况。

- [**阻塞**](/uwp/schemas/mobilebroadbandschema/wwan/element-congested) 一个布尔值，指示是否由于过度使用而强加比平时更低的连接速度。 阻塞标志表明网络当前正在 (或预期会经历) 重负载，而较低优先级的传输应推迟到其他时间（如果可能）。 您可以使用此标志来指示诸如高峰时间等概念，或响应重载的热点。

### <a name="refresh"></a>刷新

你可以根据需要将更新的设置推送到计算机，因为网络发生了更改或技术支持。 Windows 通过使用你或预配 API 提供的信息来尝试定期刷新。 可以通过来自操作员的短信通知触发刷新。 若要启用刷新，必须在预配 XML 中提供以下信息：

- [**TrustedCertificates**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-trustedcertificates) 在将来的预配文件上具有受信任签名的证书指纹列表。

- [**DelayInDays**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-delayindays) (整数) 不尝试刷新前的天数。

- [**RefreshURL**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-refreshurl) 用于获取用户预配文件的最新副本的 HTTPS URL。

- [**用户名**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-username)  & [**密码**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-password)检索重新设置文件时，使用 HTTP-Auth 显示的可选凭据。 此信息必须在存储时加密。

或者，移动宽带应用可以基于应用与操作员后端之间的通信，随时提供新的设置文件。

``` syntax
<RefreshParameters>
      <DelayInDays>30</DelayInDays>
      <RefreshURL>https://www.contoso.com/refresh</RefreshURL>
      <Username>[PLACEHOLDER]</Username>
      <Password>[PLACEHOLDER]</Password>
    </RefreshParameters>
```

### <a name="signature"></a>签名

由于预配修改了用户退出或卸载应用后保留的系统设置，因此需要对大多数 Api 进行更严格的验证。 此验证由操作员特定硬件的组合提供 (SIM) 、加密签名和用户确认。

预配要求：

|是否存在 SIM？|预配源|签名要求|用户确认要求|
|----|----|----|----|
|是，MB 提供程序|移动宽带应用|无|无|
|是，MB 提供程序|Operator 网站|证书必须：</br>-链接回受信任的根 CA。</br>-与 APN 数据库中的移动宽带硬件或体验元数据相关联。|无|
|不，Wi-Fi 提供程序|Mobile 宽带 appor 网站|证书必须：</br>-链接回受信任的根 CA。</br>-标记为进行扩展验证。|首次使用证书时，系统会提示用户确认;此后不需要确认。|

### <a name="permitted-combinations"></a>允许的组合

尽管 [**全局**](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/element-global) 模式是架构所需的唯一一级节点，但还是典型的其他节点组合。 本部分将讨论这些典型的组合：

- **配置文件 (WLANProfiles，MBNProfiles) + 计划，包括说明和使用情况** 创建或更新完整的配置文件集，并将计划信息和当前使用情况应用于每个配置文件。 如果某个配置文件引用了同一预配文件中未指定的计划，则将返回一个错误，如果该预配文件中没有配置文件引用指定的计划，则将返回警告。

- **包括说明和 (（可选）) 使用情况的计划** 更新计算机上现有配置文件的计划信息，但不修改计算机上的配置文件。 如果计算机上没有配置文件引用指定的计划，则会返回警告。

- **仅包括使用情况的计划** 更新计算机上现有配置文件中的使用情况信息，但不会修改配置文件或与每个配置文件关联的计划的描述。

## <a name="common-scenarios"></a>常见方案

下面是创建预配元数据时可能需要执行的一些常见方案：

- [查找帐户预配架构](#find-the-account-provisioning-schema)

- [向设备应用预配 XML](#apply-provisioning-xml-to-the-device)

- [预配设备以便自动连接到移动宽带网络](#provision-the-device-to-connect-automatically-to-a-mobile-broadband-network)

- [将设备设置为自动连接到 Wi-Fi 网络](#provision-the-device-to-connect-automatically-to-a-wi-fi-network)

- [将设备设置为自动连接到启用了 WISPr 的热点](#provision-the-device-to-connect-automatically-to-a-wispr-enabled-hotspot)

- [将激活发送到移动宽带设备](#sending-activation-to-the-mobile-broadband-device)

- [完成预配后，强制移动宽带设备重新连接到网络](#force-the-mobile-broadband-device-to-reconnect-to-the-network-after-provisioning-completes)

- [更新连接配置文件的数据使用情况统计信息](#updating-data-usage-statistics-for-a-connection-profile)

- [使用 SMS 消息更新数据使用情况](#update-data-usage-by-using-an-sms-message)

### <a name="find-the-account-provisioning-schema"></a>查找帐户预配架构

XSD 架构在运行 Windows 8、Windows 8.1 或 Windows 10 的任何计算机上的 **% SYSTEMROOT% \\ 架构 \\ 预配** 下可用。

### <a name="apply-provisioning-xml-to-the-device"></a>向设备应用预配 XML

可以通过使用移动宽带应用、UWP 应用或网站将预配 XML 文件应用于设备。

若要从移动宽带应用进行预配：

1. 使用 [**ProvisioningAgent**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent#Windows_Networking_NetworkOperators_ProvisioningAgent_CreateFromNetworkAccountId_System_String_)) 实例化 (的 [**ProvisioningAgent**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)实例。

2. 调用 [**ProvisionFromXmlDocumentAsync**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent#Windows_Networking_NetworkOperators_ProvisioningAgent_ProvisionFromXmlDocumentAsync_System_String_)，传入未签名的预配 XML 文档。

异步操作完成，并返回设置操作的结果。

若要从不使用 mobile 宽带应用的 UWP 应用进行预配：

1. 生成签名帐户预配 XML 文档。

2. 使用默认构造函数) 实例化 [**ProvisioningAgent**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent) 实例 (。

3. 调用 [**ProvisionFromXmlDocumentAsync**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent#Windows_Networking_NetworkOperators_ProvisioningAgent_ProvisionFromXmlDocumentAsync_System_String_)，传入已签名的 XML 文档。

异步操作完成，并返回设置操作的结果。

从网站：

1. 生成签名帐户预配 XML 文档。

2. 调用 [**msProvisionNetworks**](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85))，传入已签名的 XML 文档。

操作完成，并返回设置操作的结果。

### <a name="provision-the-device-to-connect-automatically-to-a-mobile-broadband-network"></a>预配设备以便自动连接到移动宽带网络

可以使用 **MBNProfile** 节定义预配 XML 文档。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
    <Global>
        <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
        <SubscriberId>1234567890</SubscriberId>
    </Global>
    <MBNProfiles>
      <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
          <Name>Profile Name</Name>
          <Description>The Description</Description>
          <HomeProviderName>Contoso</HomeProviderName>
          <Context>
              <AccessString>apn</AccessString>
              <UserLogonCred>
                  <UserName>username</UserName>
                  <Password>[PLACEHOLDER]</Password>
              </UserLogonCred>
          </Context>
      </DefaultProfile>
    </MBNProfiles>
</CarrierProvisioning>
```

> [!NOTE]
> **DefaultProfile** 的子元素是必需的。 有关更多详细信息，请参阅预配 XML 架构参考。

### <a name="provision-the-device-to-connect-automatically-to-a-wi-fi-network"></a>将设备设置为自动连接到 Wi-Fi 网络

可以使用 **WlanProfiles** 节定义预配 XML 文档。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <WLANProfiles>
    <WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
      <name>My Wi-Fi Hotspot</name>
      <SSIDConfig>
        <SSID>
          <name>wifihotspot1</name>
        </SSID>
      </SSIDConfig>
      <MSM>
        <security>
          <authEncryption>
            <authentication>open</authentication>
            <encryption>none</encryption>
            <useOneX>false</useOneX>
          </authEncryption>
        </security>
      </MSM>
    </WLANProfile>
  </WLANProfiles>
</CarrierProvisioning>
```

**MSM** 的子元素定义了如何连接到网络。 这包括任何必需的 EAP 配置。 支持 [WLAN \_ 配置文件架构](/windows/desktop/NativeWiFi/wlan-profileschema-schema) 中 MSM 元素的所有子元素。 有关更多详细信息，请参阅预配 XML 架构参考。

### <a name="provision-the-device-to-connect-automatically-to-a-wispr-enabled-hotspot"></a>将设备设置为自动连接到启用了 WISPr 的热点

你可以使用以下两种方式之一来启用热点身份验证：

1. 使用 **BasicAuth** 指令直接声明凭据：

    ``` syntax
    <?xml version="1.0"?>
    <CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
      <WLANProfiles>
        <WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
          <name>Contoso Wi-Fi</name>
          <SSIDConfig>
            <SSID>
              <name>Contoso Wi-Fi</name>
            </SSID>
          </SSIDConfig>
          <MSM>
            <security>
              <authEncryption>
                <authentication>open</authentication>
                <encryption>none</encryption>
                <useOneX>false</useOneX>
              </authEncryption>
              <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
                <BasicAuth>
                  <UserName>[PLACEHOLDER]</UserName>
                  <Password>[PLACEHOLDER]</Password>
                </BasicAuth>
                <TrustedDomains>
                  <TrustedDomain>hotspot.contoso.com</TrustedDomain>
                </TrustedDomains>
              </HotspotProfile>
            </security>
          </MSM>
        </WLANProfile>
      </WLANProfiles>
    </CarrierProvisioning>
    ```

2. 使用 **ExtAuth** 指令重定向到用于身份验证的应用：

    ``` syntax
    <?xml version="1.0"?>
    <CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
      <WLANProfiles>
        <WLANProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WLAN/v1">
          <name>Contoso Wi-Fi</name>
          <SSIDConfig>
            <SSID>
              <name>Contoso Wi-Fi</name>
            </SSID>
          </SSIDConfig>
          <MSM>
            <security>
              <authEncryption>
                <authentication>open</authentication>
                <encryption>none</encryption>
                <useOneX>false</useOneX>
              </authEncryption>
              <HotspotProfile xmlns="http://www.microsoft.com/networking/WLAN/HotspotProfile/v1">
                <ExtAuth>
                  <ExtensionId>Alice</ExtensionId>
                </ExtAuth>
                <TrustedDomains>
                  <TrustedDomain>hotspot.contoso.com</TrustedDomain>
                </TrustedDomains>
              </HotspotProfile>
            </security>
          </MSM>
        </WLANProfile>
      </WLANProfiles>
    </CarrierProvisioning>
    ```

应尽可能直接定义凭据。 重定向到另一个应用具有强大的功能和复杂性。

### <a name="sending-activation-to-the-mobile-broadband-device"></a>将激活发送到移动宽带设备

[**CarrierSpecificData**](/uwp/schemas/mobilebroadbandschema/wwan/element-carrierspecificdata)元素内包含的任意二进制大型对象 (BLOB) 可以使用 ProvisioningAgent 进行 Base64 编码并发送到设备。 可以通过在预配 XML 中 **使用 &lt; Activation &gt; ServiceActivatation** 指令来完成此操作：

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <Activation>
    <ServiceActivation xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
      <CarrierSpecificData>YXJiaXRyYXJ5ZGF0YQ==</CarrierSpecificData>
    </ServiceActivation>
  </Activation>
</CarrierProvisioning>
```

此方法等效于调用移动宽带 API 的 [**IMbnVendorSpecificOperation：： SetVendorSpecific**](/windows/win32/api/mbnapi/nf-mbnapi-imbnvendorspecificoperation-setvendorspecific) 方法，并将 SAFEARRAY 传递到 BLOB 内容。

### <a name="force-the-mobile-broadband-device-to-reconnect-to-the-network-after-provisioning-completes"></a>完成预配后，强制移动宽带设备重新连接到网络

可以通过两种方式强制移动宽带设备在预配后重新连接到网络： **ReregisterToNetwork** 和 **ReconnectToNetwork**。

可以使用 **ReregisterToNetwork** 指令强制通过关闭移动宽带无线电并重新注册到移动宽带网络，然后再重新注册。 无线电返回后，适配器将通过使用默认配置文件进行连接。 应慎用此指令，且仅当帐户激活后需要从网络取消注册时才使用此指令。

当上下文激活必须在帐户激活完成后应用任何新安全或策略设置时，可以使用 **ReconnectToNetwork** 指令。 这是通过停用 PDP 上下文并基于移动宽带适配器的默认配置文件设置重新激活来完成的。 如果在同一预配 XML 中更新了默认配置文件，则将使用新的配置文件设置。

还可以选择使用重试计数/间隔和延迟执行时间来指定这些指令。

> [!NOTE]
> 如果在 **ReregisterToNetwork** 中成功地循环了无线电，但使用默认配置文件自动连接回网络失败，则后续重试不会再次循环广播。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{00000000-1111-2222-3333-444444444444}</CarrierId>
    <SubscriberId>1234567890</SubscriberId>
  </Global>
  <Activation>
      <!-- Cycle the radio and reconnect to the default profile with an 
           initial execution delay of 30 seconds and retries every 1 minute 
           up to 3 times.
           -->
      <ReregisterToNetwork
          xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1"
          Delay="PT30S"
          RetryCount="3"
          RetryInterval="PT1M"
          />
  </Activation>
</CarrierProvisioning>
```

### <a name="updating-data-usage-statistics-for-a-connection-profile"></a>更新连接配置文件的数据使用情况统计信息

仅可通过应用新的帐户预配文件（具有更新的计划信息）来更新通过使用 [**ProvisioningAgent**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent) 预配的配置文件的使用情况。 你可以提供仅包含使用情况信息的设置文件，或仅包含计划信息。 根据要更改的系统配置的数量，新的预配文件可能包含以下内容：

- 配置文件、计划说明和使用情况

-  (更新现有配置文件的计划说明和使用情况) 

- 计划使用情况 (更新现有配置文件和计划) 

如果应用新的配置文件和未在 XML 中定义的引用计划，设置结果将包括警告。

### <a name="update-data-usage-by-using-an-sms-message"></a>使用 SMS 消息更新数据使用情况

可以通过以下方式之一完成此操作：

- 指定操作员消息，接收操作员通知消息，使用 SMS API 读取消息，分析应用程序中的消息，然后通过使用 **IProvisionedProfile** 设置使用情况。

- 指定具有有效的使用字段组合的操作员消息规则，并直接在短信中提供更新的使用情况。

## <a name="troubleshooting"></a>疑难解答

如果遇到预配问题，你可以使用以下部分来帮助你解决问题。

### <a name="provisioning-api-results"></a>预配 API 结果

如果预配失败，则在尝试执行设置操作时将收到异常。 可能导致异常的故障包括：

- 预配 XML 不符合 [CarrierControlSchema 架构](/uwp/schemas/mobilebroadbandschema/carriercontrolschema/schema-root)。

- 预配 XML 需要签名，但未进行正确签名。

### <a name="partial-provisioning-failures"></a>部分预配失败

由于各种原因，预配操作部分可能不会成功。 例如，你可能有一个对在预配时未提供 Wi-Fi 硬件的引用。 预配代理会尽力尝试预配文件中的所有内容。 如果出现故障，则会在使用 [**ProvisionFromXmlDocumentAsync**](/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent#Windows_Networking_NetworkOperators_ProvisioningAgent_ProvisionFromXmlDocumentAsync_System_String_)异步返回的预配结果中进行说明。

结果以 XML 形式返回，并可进行分析以发现失败。 元素提供结构以显示失败的内容， **错误代码** 属性以标准 HRESULT 的形式指示失败的原因。

例如，以下错误代码表明未预配 wlan 配置文件，因为 WLAN 服务处于非活动状态：

``` syntax
<CarrierProvisioningResult>
    <WLANProfiles ErrorCode=”80070426”/>
</CarrierProvisioningResult>
```

如果无法应用单个配置文件，它将如下所示：

``` syntax
<CarrierProvisioningResult>
    <WLANProfiles>
        <WLANProfile Name=”MyProfile” ErrorCode=”80070005”/>
    </WLANProfiles>
</CarrierProvisioningResult>
```

### <a name="event-logs"></a>事件日志

**应用程序和服务中的事件记录 \\ Microsoft \\ Windows \\ NetworkProvisioning \\ 操作** 通道可提供有关预配失败的详细反馈。

### <a name="powershell-provisioningtesthelper-module"></a>PowerShell ProvisioningTestHelper 模块

你可以从 Windows 8、Windows 8.1 和 Windows 10 Sdk 导入 **ProvisioningTestHelper** 模块。 通过使用此模块，您可以生成和安装 EV 证书，使用已安装的证书对 XML 文件进行签名，并根据预配架构验证 XML。 若要将模块导入到 PowerShell 会话中，请键入以下命令：

``` syntax
Import-Module "<path_to_sdk>\bin\<arch>\ProvisioningTestHelper.psd1"
```

其中， &lt; *\_ \_ \\ \\ &lt; sdk bin 的路径是 windows 8、Windows 8.1 或 windows 10 sdk 的安装位置，它们对应于计算机的体系结构。 &gt;* &gt;

导入此模块后，以下四个 PowerShell cmdlet 可用：

- **安装-TestEVCert** 生成新的 CA 证书，在测试计算机上将其注册为受信任的 EV SSL 提供程序，并使用它生成并安装 EV 证书以用于签名。 必须只运行一次此 cmdlet 来安装证书。 您可以使用证书对任意数量的文件进行签名。

    ``` syntax
    Install-TestEVCert -CertName <Certificate Name> -RootCertOutputPath <complete path to the folder to which the root certificate is to be exported>
    ```

    该客户端证书的名称与命令中指定的名称相同，并且根证书将 "Root" 与客户端证书名称一起附加到该证书。 *-CertName* 参数是可选的。 如果未指定– CertName 参数，则使用 **MBAPTestCert** 。

    *-RootCertOutputPath* 参数也是可选的。 如果要使用 Install-RootCertFromFile cmdlet 导出要安装在另一台计算机上的根证书，则应使用此方法。

- **安装-RootCertFromFile** 在另一台计算机上应用测试根证书，以测试开发计算机以外的计算机上的客户端体验。

    ``` syntax
    Install-RootCertFromFile -CertFile <complete path to the root certificate>
    ```

- **Convertto-html-SignedXml** 使用 (为测试生成的 EV 证书，或由第三方提供程序颁发的 EV 证书) 将 XML-DSig 签名应用于预配 XML 文件。 受信任的证书中的此签名会导致 Windows 将预配文件从没有关联硬件的移动宽带应用接受为有效。

    ``` syntax
    ConvertTo-SignedXml -InputFile <complete path to the input XML file> -OutputFile <complete path to the output XML file> -CertName <name of the certificate used to sign the xml>
    ```

    此命令将对输入 XML 文件进行签名，将签名放入 XML，并将其保存到输出 XML 文件。

- **ValidProvisioningXml** 针对预配架构验证预配 XML (有符号或无符号) 。

    ``` syntax
    Test-ValidProvisioningXml -InputFile <complete path to the input XML file>
    ```