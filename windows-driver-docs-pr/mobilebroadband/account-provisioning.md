---
title: 帐户预配
description: 帐户预配
ms.assetid: 3ffcd769-253f-4918-8095-a9206445a201
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61395fc97cbb93c63c93226ac8904fbd216a70fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547291"
---
# <a name="account-provisioning"></a>帐户预配


预配是指配置 Windows 计算机连接到运营商网络所需的信息。 移动宽带订阅购买后通常执行预配。 Windows 接受来自运算符的基于 XML 的预配文件。 预配 API 应用的置备 XML 文件从该运算符，通过使用移动宽带应用或通过采购网站。

下图说明的内容和置备 XML 文件的层次结构。

![预配的 xml 文件层次结构](images/mb-provisioningmetadata.jpg)

有关预配的架构的详细信息，请参阅[CarrierControlSchema 架构](https://msdn.microsoft.com/library/windows/apps/hh868312)。

## <a name="span-idupdatingtheprovisioningmetadataspanspan-idupdatingtheprovisioningmetadataspanspan-idupdatingtheprovisioningmetadataspanupdating-the-provisioning-metadata"></a><span id="Updating_the_provisioning_metadata"></span><span id="updating_the_provisioning_metadata"></span><span id="UPDATING_THE_PROVISIONING_METADATA"></span>更新预配的元数据

有几种方法可以更新的计算机上预配的元数据。

### <a name="span-idmobilebroadbandappspanspan-idmobilebroadbandappspanspan-idmobilebroadbandappspanmobile-broadband-app"></a><span id="Mobile_broadband_app"></span><span id="mobile_broadband_app"></span><span id="MOBILE_BROADBAND_APP"></span>移动宽带应用

在计算机上安装的移动宽带应用后，它可以检索或生成更新的预配文件根据应用程序中实现任何触发器。

移动宽带应用程序可以使用的应用预配文件[ **Windows.Networking.NetworkOperator.ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397) Api。 如果应用程序与网络帐户 ID，它可以使用[ **CreateFromNetworkAccountId** ](https://msdn.microsoft.com/library/windows/apps/br207398)以提供无符号的元数据。 如果应用不与网络帐户 ID 相关联，它必须使用的默认构造函数**ProvisioningAgent**和 XML 签名。

移动宽带应用可以使用以下触发器更新的预配的元数据：

-   **使用情况**最初配置的数据限制后，可以告知 Windows 通知每个 5%的使用率增量处的应用。 这可确保应用程序检索的最新的使用情况信息。

-   **计时器**计时器可以在适当的时间间隔更新的预配的元数据。

-   **传入的 SMS**可以发送短信能够理解您的应用程序。 这可能会定义一条消息，启动了刷新，或自动检查收到的阈值通知后更新使用情况。

-   **Windows 通知服务**Any UWP 应用可以注册推送通知，并根据其内容执行操作。 可用作此通知通道进行预配的更新。

-   **大型位置更改**不同的参数将应用于不同的区域设置中，如果更改了位置可能会触发应用程序要应用的用户的新位置更新的设置。

-   **时区更改**有关大型区域的大小，系统时区中的更改可用于为代理位置更改。 这可以是在没有 GPS 或移动宽带的计算机上特定的感兴趣。

### <a name="span-idweb-basedprovisioningspanspan-idweb-basedprovisioningspanspan-idweb-basedprovisioningspanweb-based-provisioning"></a><span id="Web-based_provisioning"></span><span id="web-based_provisioning"></span><span id="WEB-BASED_PROVISIONING"></span>基于 web 的预配

网站可以使用提供预配数据[ **window.external.msProvisionNetworks** ](https://msdn.microsoft.com/library/hh848316) API。 预配到此 API 提供的文件时，必须使用 X.509 证书和 XML DSig 进行签名。

通过使用 APN 数据库、 服务元数据或预配的元数据文件的上一个帐户，可以预先提供到计算机证书。 如果证书已是受信任的则无需用户交互。 如果证书以前不被透露给计算机，它必须是 EV 证书，并接受证书前，提示用户同意的情况下输入。

### <a name="span-idautomaticprovisioningrefreshspanspan-idautomaticprovisioningrefreshspanspan-idautomaticprovisioningrefreshspanautomatic-provisioning-refresh"></a><span id="Automatic_provisioning_refresh"></span><span id="automatic_provisioning_refresh"></span><span id="AUTOMATIC_PROVISIONING_REFRESH"></span>自动预配的刷新

预配文件可以包括 Windows 自动检索更新的预配文件在计划的时间间隔或在响应特定的 SMS 消息中的指令。 此方法不需要在本地计算机上安装移动宽带应用。

## <a name="span-idapmdconspanspan-idapmdconspanprovisioning-metadata-contents"></a><span id="apmdcon"></span><span id="APMDCON"></span>预配的元数据内容


预配的元数据包括以下各节：

-   [全局](#global)

-   [激活](#activation)

-   [移动宽带信息](#mobile-broadband-information)

-   [Wi-fi 信息](#wi-fi-information)

-   [计划信息](#plan-information)

-   [刷新](#refresh)

-   [签名](#signature)

-   [允许的组合](#permitted-combinations)

有关这两部分的详细信息，请参阅[CarrierControlSchema 架构](https://msdn.microsoft.com/library/windows/apps/hh868312)。

### <a name="global"></a>全局

在预配的每个文件中需要的全局部分。 在本部分中的必需的元素如下所示：

- [**CarrierId** ](https://msdn.microsoft.com/library/windows/apps/hh868288)唯一标识编写该文件的组织的 GUID。 如果要构建移动宽带应用程序，则必须使用中指定的 GUID[服务号码](https://msdn.microsoft.com/library/windows/hardware/dn236413)字段**ServiceInfo.xml**服务元数据包中。 有关服务的元数据包架构的信息，请参阅[服务的元数据数据包架构参考](service-metadata-package-schema-reference.md)。

  > [!NOTE]
  > 这是你在中提供的相同服务号**创建移动宽带体验向导**Windows 开发人员中心仪表板 – 硬件上。
  > 如果不创建移动宽带应用，可以生成你的组织使用的 GUID。 在任一情况下，应始终使用您的组织颁发的所有预配文件相同的 GUID。

- [**SubscriberId** ](https://msdn.microsoft.com/library/windows/apps/hh868305)唯一标识你的组织中的客户的字符串。 如果你是移动运营商，这应该是 GSM 运算符的 IMSI 或 ICCID 范围、 提供程序 ID 或 CDMA 运算符的提供程序名称。 如果您不是移动运营商，可以选择任何足够唯一的字符串。

### <a name="activation"></a>激活

激活过程完成后端后，会出现设备激活。 PC 可能需要连接到网络之前按照特定的指令。 预配引擎使用的设备激活元素中收到的激活说明。 如果未不指定任何值，则不不需要任何客户端操作。 可用的操作包括：

-   **重新连接**断开连接并连接到运营商网络。

    **重新注册**断开连接并注册到运营商网络。

-   **数据**数据或你想要发送到设备以激活连接的说明。 预配引擎将此数据按原样向设备传递。 有关 CDMA，这可以包括说明如下所述 **\*228**用于启动 OTA 编程会话重新连接到网络。

### <a name="mobile-broadband-information"></a>移动宽带信息

移动宽带信息包含多个元素：

[**MBNProfiles**](https://msdn.microsoft.com/library/windows/apps/hh868295)

移动运营商网络上定义订阅服务器的信息。 有两个不同的配置文件，可以使用：

-   [**PurchaseProfile**](https://msdn.microsoft.com/library/windows/apps/hh868301):连接到操作员的网络，以购买新的订阅所需的信息。

-   [**DefaultProfile** ](https://msdn.microsoft.com/library/windows/apps/hh868290)每个移动宽带订阅可以有一个用于连接到家庭网络运算符的默认配置文件。 Windows 连接管理器使用此配置文件进行自动连接到网络。

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
              <Password>mbpass</Password>
            </UserLogonCred>
          </Context>
        </DefaultProfile>
      </MBNProfiles>
    ```

[**品牌**](https://msdn.microsoft.com/library/windows/apps/hh868446)

> [!IMPORTANT]
> 从 Windows 10，版本 1709，开始 ProvisioningAgent API 由预配的品牌字段已替换为品牌 COSA 数据库中的字段。 **徽标**已被取代**品牌图标**中 COSA，和**名称**已由**品牌名称**COSA 中。
>
> **徽标**并**名称**在 Windows 10 版本 1709年及更高版本中预配时将不再被视为。 ProvisioningAgent API 不会引发错误，如果使用，但您应更改**品牌图标**并**品牌名称**中 COSA 相反。  
>
> 有关详细信息**品牌图标**并**品牌名称**，请参阅[桌面 COSA/APN 数据库设置 （桌面 COSA 仅设置）](desktop-cosa-apn-database-settings.md#desktop-cosa-only-settings)。

品牌可让你指定如何在 Windows 中显示你的移动宽带网络。 此信息将覆盖任何服务的元数据，如果存在。 如果未不提供任何信息，将使用服务元数据包的内容。 标记的元素如下所示：

-   [**徽标**](https://msdn.microsoft.com/library/windows/apps/hh868460) Base64 编码。PNG 或。在 XML 中嵌入的 BMP 文件。 此徽标将应用到移动宽带配置文件在网络列表中进行显示。

-   [**名称**](https://msdn.microsoft.com/library/windows/apps/hh868463)设置移动宽带的配置文件的运营商的显示名称。

**SMS 分析**

你可以设置规则，以标识一条短信和提取信息作为置备 XML 文件的一部分。 要更新的数据使用情况统计信息或启动的设置信息的刷新，可以使用 SMS 消息。 这些消息可以通过下列组合进行标识：

-   持有者类型 (短信/USSD)

-   发件人 (仅 SMS)

-   正则表达式

短信通知的详细信息，请参阅[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

每个规则包含以下信息：

- **无提示**如果此值为 true，消息将导致[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)仅事件。 如果此值为 false，消息将导致**SmsMessageReceived**事件。

- **允许发件人**指定通知允许到达保留发件人地址。 此数字必须与发件人号码接收 SMS 消息，包括国际格式中的完全匹配。

- **模式**正则表达式以标识和 （可选） 的文本消息中提取数据字段。 此模式将匹配所有消息的发件人： `[^]*`

- **RuleId**作为的一部分传递到移动宽带应用此规则的标识符[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件。 此标识符可让应用知道哪些规则导致 SMS 来触发 MobileOperatorNotification 事件，并可以减少应用程序的需要再次分析消息。

- **字段和组**正则表达式模式中的每个捕获组绑定到命名的字段。 这用于提取和数据转换为一组可用值。 例如，可将第一个匹配项组绑定到**使用情况**字段和第二个匹配项的组可以绑定到**UsageDataLimit**字段。 此关联指示第一个值是当前的使用情况信息，并且第二个值的最大允许的用法。

  - **使用情况，UsagePercentage，UsageOverage，UsageOveragePercentage**:为绝对数字，以占数据限制，为对数据限制，超出的数字或百分比值超过数据限制，则表示当前使用情况。 绝对值可以引用指定度量单位，该值表示在其中一个组。

  - **UsageTimestamp**:日期和时间计算用法字段中。 如果有此信息必须包含**使用情况\\*** 字段是包含。 格式字符串包含来表达应如何解释子字符串的以下标识符：

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>标识符</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>%d</p></td>
    <td><p>每月的某一日，十进制数字 (01 – 31)</p></td>
    </tr>
    <tr class="even">
    <td><p>%H</p></td>
    <td><p>小时，24 小时制 (00 – 23)</p></td>
    </tr>
    <tr class="odd">
    <td><p>%I</p></td>
    <td><p>小时采用 12 小时格式 (01 – 12)</p></td>
    </tr>
    <tr class="even">
    <td><p>%m</p></td>
    <td><p>月份，十进制数字 (01 – 12)</p></td>
    </tr>
    <tr class="odd">
    <td><p>%M</p></td>
    <td><p>分钟，十进制数字 (00 – 59)</p></td>
    </tr>
    <tr class="even">
    <td><p>%S</p></td>
    <td><p>秒，小数形式 (00 – 59)</p></td>
    </tr>
    <tr class="odd">
    <td><p>%y</p></td>
    <td><p>不带世纪的年份，十进制数字 (00 – 99)</p></td>
    </tr>
    <tr class="even">
    <td><p>%Y</p></td>
    <td><p>带世纪，以十进制数 (0000-9999) 的年份</p></td>
    </tr>
    <tr class="odd">
    <td><p>%p</p></td>
    <td><p>AM/PM 指示符</p></td>
    </tr>
    <tr class="even">
    <td><p>%#d、 %#H、 %#I，%#m、 %#M、 %#S、 %#y，%#Y</p></td>
    <td><p>与上述相同但包含没有前导零</p></td>
    </tr>
    </tbody>
    </table>

         

  - **DataLimit**:绝对允许用户使用; 的字节数这包括指定用于表示值的单位的组。

  - **OverDataLimit，拥塞**:修改报告给应用程序以指示用户已超出其数据限制或网络负载较重的标志。

  - **InboundBandwidth、 OutboundBandwidth**:如果在最大带宽施加的网络，此参数指定值和度量单位表示的组。

  - **PlanType**:指定用户为后续使用量的收费方式。

**谨慎**  因为短信影响 Windows 行为，仅受信任可以使用 SMS 消息。 通过限制发件人地址维护安全性。 此安全方法假定该网络的 SMS 网关可确保消息来自受限制的发件人不会受到欺骗。

 

### <a name="wi-fi-information"></a>Wi-fi 信息

此部分中，你可提供任意数量的 Wi-fi 网络配置文件的 Windows 使用。 部分的格式是类似于 Windows 本机 WLAN API 使用的 XML 架构。

**请注意**  一个配置文件可以包含多个 Ssid，如果所有其他设置相同。 如果不同的网络以其他方式 （身份验证方法、 加密设置、 计划等） 各不相同，则必须创建附加的配置文件。

 

当指定 WLAN 部分时，还必须指定应在计算机配置的所有配置文件。 如果这些配置文件引用一个数据计划，还必须包含的计划部分。 本部分中进行处理时，会发生的行为如下所示：

-   如果计算机具有不能再指定的配置文件，则将其删除。

-   如果指定的配置文件，它是更新还是创建。

-   WLAN 部分为空将删除所有配置文件。

-   省略 WLAN 部分保持不变的计算机上留出 WLAN 配置文件。

在本部分中的其他节点是关联的计划。 此节点使 Windows 能够 WLAN 配置文件相关联的计划中的计划部分所述。 该计划可以告知 Windows 网络的计数的状态，并在计算机连接到网络的时间段内影响的 Windows 行为。

**未加密的网络，不自动进行身份验证**

此配置文件配置 Windows 以连接到一个开放的网络。

-   如果此网络包含强制网络门户，浏览器打开时连接到网络。

-   如果网络不包含强制网络门户，用户连接与任何进一步的操作。

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

**未加密的网络，WISPr 身份验证**

此配置文件配置 Windows 以连接到一个开放的网络，并使用漫游 (WISPr) 身份验证的无线 Internet 服务提供商：

-   如果网络包含 WISPr 能够强制网络门户，指定的用户名和密码提交到指定的身份验证服务器。

-   如果不能 WISPr 强制网络门户，浏览器打开时连接到网络。

-   如果网络不包含强制网络门户，用户连接与任何进一步的操作。

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
        <Password>password1</Password>
        <TrustedDomains>
          <TrustedDomain>www.contosoportal.com</TrustedDomain>
        </TrustedDomains>
      </HotspotProfile>
    </security>
  </MSM>
</WLANProfile>
```

**加密的网络，EAP SIM 身份验证**

此配置文件配置 Windows SIM 使用作为身份验证类型，例如热点 2.0 网络连接到的加密网络。 热点 2.0 定义此类网络以用于 EAP SIM 身份验证的 WPA2-企业。

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

**未加密的网络，基于应用的身份验证**

此配置文件配置 Windows 连接到一个开放的网络和中与你的移动宽带应用协作使用 WISPr 身份验证。

-   如果网络包含强制网络门户，在后台提供 WISPr 凭据打开您的应用程序。 凭据然后提交到指定的身份验证服务器。

-   如果不能 WISPr 强制网络门户，浏览器打开时连接到网络。

-   如果网络不包含强制网络门户，用户连接与任何进一步的操作。

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

每个移动宽带和热点配置文件引用一个计划。 多个配置文件可以引用相同的计划。 计划单独的顶级部分所述。

计划分为两个部分 —*描述*并*用法*。 这允许您最初提供配置文件和说明，在更大的预配文件，并随后提供包含客户的当前用量较小的预配文件。

此信息用于直接影响行为的 Windows，并提供给应用程序定制其行为到网络。 此信息可通过网络信息 Api 的第三方应用程序。

### <a name="description"></a>描述

通常通过客户的订阅期限，更改频率较低的元素包括：

-   [**PlanType** ](https://msdn.microsoft.com/library/windows/apps/hh868468)的客户所具有的与运算符的计费关系的类型：

    -   **不受限制**使用情况不会产生额外费用。

    -   **修复了**用户分配给一定数量的固定成本的使用情况。

    -   **变量**用户需根据使用情况付费。

-   [**SecurityUpdatesExempt** ](https://msdn.microsoft.com/library/windows/apps/hh868374)布尔值，该值指定是否安全更新计入客户的使用情况。

-   [**DataLimitInMegabytes** ](https://msdn.microsoft.com/library/windows/apps/hh868367)用户的分配使用情况，如果[ **PlanType** ](https://msdn.microsoft.com/library/windows/apps/hh868468)是**固定**。

-   [**BillingCycle** ](https://msdn.microsoft.com/library/windows/apps/hh868366)定义该计划的起始日期和时间，其持续时间，以及在计费周期结束时会发生什么情况。

-   [**BandwidthInKbps** ](https://msdn.microsoft.com/library/windows/apps/hh868343)作为允许的网络的用户的连接速度; 这可以反映其计划的标准或反映当前所规定的运营商由于拥塞或过多使用 （最大 2 Gbps） 较低的速率。

-   [**MaxTransferSizeInMegabytes** ](https://msdn.microsoft.com/library/windows/apps/hh868371)一个整数，表示与兼容应用程序应允许通过按流量计费的连接，无需显式用户批准使用的连接的单独下载的大小。

-   [**UserSMSEnabled** ](https://msdn.microsoft.com/library/windows/apps/hh868376)指示计划是否包括用户-短信支持。 如果为 true，Windows 将保留设备附加到连接待机状态中的网络，即使不使用移动宽带接口。 当计算机处于空闲状态时，如果为 false，Windows 可以关闭省电的移动宽带接口，从而不产生的设备中的可通过网络寻址。

### <a name="usage"></a>用法

较高的频率可以更改以下元素：

-   [**UsageInMegabytes** ](https://msdn.microsoft.com/library/windows/apps/hh868350)用户的最新数据使用情况。

-   [**OverDataLimit** ](https://msdn.microsoft.com/library/windows/apps/hh868465)布尔值，该值指示用户是否已通过分配使用情况，如果[ **PlanType** ](https://msdn.microsoft.com/library/windows/apps/hh868468)是**固定**。

-   [**拥塞**](https://msdn.microsoft.com/library/windows/apps/hh868449)布尔值，该值指示是否在较低的连接速度比平常施加由于过多的使用情况。 Congested 标志指示网络目前遇到 （或期望） 沉重负载时，和优先级较低的传输应延迟到另一个时间，在可能的情况。 可以使用此标志，以指示概念，如高峰时间或响应重载热点。

### <a name="refresh"></a>刷新

由于网络更改或技术支持，可以推送到所需的计算机的更新的设置。 Windows 会定期刷新尝试通过使用由你或预配 API 提供的信息。 可以通过从运算符的短信通知触发刷新。 若要启用刷新，必须提供预配 XML 中的以下信息：

-   [**TrustedCertificates** ](https://msdn.microsoft.com/library/windows/apps/hh868307)具有受信任在将来的预配文件签名的证书指纹的列表。

-   [**DelayInDays** ](https://msdn.microsoft.com/library/windows/apps/hh868291) （整数） 数的刷新将不尝试在其之前的天数。

-   [**RefreshURL** ](https://msdn.microsoft.com/library/windows/apps/hh868303)的 HTTPS URL，以获取用户的最新副本的预配文件。

-   [**用户名**](https://msdn.microsoft.com/library/windows/apps/hh868308) & [**密码**](https://msdn.microsoft.com/library/windows/apps/hh868297)检索重新预配文件时使用 HTTP 身份验证的呈现的可选凭据。 此信息必须以加密形式存储。

-   

或者，移动宽带应用程序可以提供新的预配文件在任何时候，根据应用程序和操作员的后端之间的通信。

``` syntax
<RefreshParameters>
      <DelayInDays>30</DelayInDays>
      <RefreshURL>https://www.contoso.com/refresh</RefreshURL>
      <Username>foo</Username>
      <Password>bar</Password>
    </RefreshParameters>
```

### <a name="signature"></a>签名

预配修改后用户已退出或卸载应用程序保留的系统设置，因为更严格的验证度量值都需要比大多数 Api。 此验证提供的特定于运算符的硬件 (SIM)、 加密签名和用户进行确认的组合。

预配要求：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>SIM 存在？</th>
<th>预配的源</th>
<th>签名要求</th>
<th>用户确认要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是的 MB 提供程序</p></td>
<td><p>移动宽带应用</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>是的 MB 提供程序</p></td>
<td><p>运算符 web 站点</p></td>
<td><p>证书必须：</p>
<ul>
<li><p>返回到受信任的根 CA 链...</p></li>
<li><p>与 APN 数据库中的移动宽带硬件相关联，或者遇到元数据。</p></li>
</ul></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>否，Wi-fi 提供程序</p></td>
<td><p>移动宽带 appor web 站点</p></td>
<td><p>证书必须：</p>
<ul>
<li><p>返回到受信任的根 CA 链。</p></li>
<li><p>对于扩展验证标记。</p></li>
</ul></td>
<td><p>系统会提示用户确认第一次使用该证书;未确认之后是必需的。</p></td>
</tr>
</tbody>
</table>

 

### <a name="permitted-combinations"></a>允许的组合

尽管[ **Global** ](https://msdn.microsoft.com/library/windows/apps/hh868294)是仅第一级节点所需的架构，通常会有其他节点的某些组合。 本部分讨论这些典型的组合：

-   **配置文件 （WLANProfiles，MBNProfiles） + 计划包括说明和使用情况**创建或更新完整设置的配置文件，并应用计划信息，以及每个当前使用情况。 如果一个配置文件引用在同一配置文件中，未指定的计划，如果没有配置文件预配文件中的引用指定的计划，则返回一条警告，则返回错误。

-   **计划包括说明和 （可选） 使用情况**现有更新计划信息的计算机上，配置文件，但不会修改在计算机上的配置文件。 如果在计算机上的没有配置文件引用指定的计划，则返回一条警告。

-   **计划仅包括使用情况**更新现有配置文件中的计算机上，使用情况信息，但不会修改配置文件或与每个配置文件相关联的计划的说明。

## <a name="span-idcommonscenariosspanspan-idcommonscenariosspanspan-idcommonscenariosspancommon-scenarios"></a><span id="Common_Scenarios"></span><span id="common_scenarios"></span><span id="COMMON_SCENARIOS"></span>常见方案


下面是在创建预配的元数据可能需要一些常见方案：

-   [查找帐户预配架构](#find-the-account-provisioning-schema)

-   [将应用到设备预配 XML](#apply-provisioning-xml-to-the-device)

-   [预配设备自动连接到移动宽带网络](#provision-the-device-to-connect-automatically-to-a-mobile-broadband-network)

-   [预配设备以自动连接到 Wi-fi 网络](#provision-the-device-to-connect-automatically-to-a-wi-fi-network)

-   [预配设备自动连接到启用了 WISPr 的热点](#provision-the-device-to-connect-automatically-to-a-wispr-enabled-hotspot)

-   [将激活发送到移动宽带设备](#sending-activation-to-the-mobile-broadband-device)

-   [强制移动宽带设备预配完成后重新连接到网络](#force-the-mobile-broadband-device-to-reconnect-to-the-network-after-provisioning-completes)

-   [更新连接配置文件的数据使用情况统计信息](#updating-data-usage-statistics-for-a-connection-profile)

-   [使用短信更新数据使用情况](#update-data-usage-by-using-an-sms-message)

### <a name="find-the-account-provisioning-schema"></a>查找帐户预配架构

XSD 架构下有 **%SYSTEMROOT%\\架构\\预配**运行 Windows 8、 Windows 8.1 或 Windows 10 的任何计算机上。

### <a name="apply-provisioning-xml-to-the-device"></a>将应用到设备预配 XML

通过使用移动宽带应用程序，即 UWP 应用，或从网站上，可以应用到设备的置备 XML 文件。

若要从移动宽带应用预配：

1.  实例化[ **ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397)实例 (通过使用[ **Windows.Networking.NetworkOperators.ProvisioningAgent.CreateFromNetworkAccountId**](https://msdn.microsoft.com/library/windows/apps/br207398)).

2.  调用[ **ProvisionFromXmlDocumentAsync**](https://msdn.microsoft.com/library/windows/apps/br207400)、 传入无符号的置备 XML 文档。

返回异步操作完成和预配操作的结果。

若要从 UWP 应用之外的移动宽带应用预配：

1.  生成已签名的帐户预配 XML 文档。

2.  实例化[ **ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397) （通过使用默认构造函数） 的实例。

3.  调用[ **ProvisionFromXmlDocumentAsync**](https://msdn.microsoft.com/library/windows/apps/br207400)、 传入已签名的 XML 文档。

在异步操作完成并返回预配操作的结果。

从网站：

1.  生成已签名的帐户预配 XML 文档。

2.  调用[ **window.external.msProvisionNetworks**](https://msdn.microsoft.com/library/hh848316)、 传入已签名的 XML 文档。

在操作完成并返回预配操作的结果。

### <a name="provision-the-device-to-connect-automatically-to-a-mobile-broadband-network"></a>预配设备自动连接到移动宽带网络

可以通过使用定义的预配的 XML 文档**MBNProfile**部分。

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
                  <Password>password</Password>
              </UserLogonCred>
          </Context>
      </DefaultProfile>
    </MBNProfiles>
</CarrierProvisioning>
```

**请注意**  的子元素**DefaultProfile**所需。 请参阅更多详细信息的预配 XML 架构引用。

 

### <a name="provision-the-device-to-connect-automatically-to-a-wi-fi-network"></a>预配设备以自动连接到 Wi-fi 网络

可以通过使用定义的预配的 XML 文档**WlanProfiles**部分。

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

子元素**MSM**定义如何连接到网络。 这包括任何必需的 EAP 配置。 MSM 元素中的所有子元素[WLAN\_配置文件架构](https://msdn.microsoft.com/library/windows/desktop/ms707341)支持。 请参阅更多详细信息的预配 XML 架构引用。

### <a name="provision-the-device-to-connect-automatically-to-a-wispr-enabled-hotspot"></a>预配设备自动连接到启用了 WISPr 的热点

可以使用启用热点身份验证的以下两种方法之一：

1.  直接使用声明凭据**BasicAuth**指令：

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
                  <UserName>Alice</UserName>
                  <Password>secret</Password>
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

2.  使用重定向到身份验证的应用程序**ExtAuth**指令：

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

您应直接定义凭据在可能的情况。 将重定向到另一个应用程序有能力和复杂性的影响。

### <a name="sending-activation-to-the-mobile-broadband-device"></a>将激活发送到移动宽带设备

任意二进制大型对象 (BLOB) 中包含[ **CarrierSpecificData** ](https://msdn.microsoft.com/library/windows/apps/hh868447)元素可以通过使用 ProvisioningAgent 是 Base64 编码，然后发送到设备。 您可以执行此操作通过使用**激活&lt;ServiceActivatation&gt;** 中置备 XML 指令：

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

此方法等效于调用[ **IMbnVendorSpecificOperation::SetVendorSpecific** ](https://msdn.microsoft.com/library/windows/desktop/dd323208)的移动宽带 API，并传递 SAFEARRAY 以及将 BLOB 内容的方法。

### <a name="force-the-mobile-broadband-device-to-reconnect-to-the-network-after-provisioning-completes"></a>强制移动宽带设备预配完成后重新连接到网络

有两种方法可以强制执行移动宽带设备预配后重新连接到网络：**ReregisterToNetwork**并**ReconnectToNetwork**。

可以使用**ReregisterToNetwork**指令以强制重新注册到移动宽带网络通过关闭移动宽带单选，然后再打开。 单选回来后，适配器将连接通过使用默认配置文件。 在尽量少，且仅应使用此指令是否需要能够从网络帐户激活后取消注册。

可以使用**ReconnectToNetwork**指令时上下文激活帐户激活完成后必须将任何新的安全或策略设置的应用。 这是通过停用 PDP 上下文和重新激活基于移动宽带卡的默认配置文件设置。 如果相同的预配 XML 中更新的默认配置文件时，将使用新的配置文件设置。

或者，您可以指定通过使用这些指令重试计数/时间间隔和延迟执行时间。

**请注意**  如果单选成功中靠**ReregisterToNetwork**但自动返回到使用默认配置文件的网络连接失败，则后续重试不循环单选电子邮件了。

 

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

您只能更新通过使用预配配置文件的使用情况[ **ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397)通过应用新的帐户预配已更新计划信息的文件。 可以提供一个预配文件，包含仅使用情况信息，或仅计划信息。 具体取决于多少你想要更改的系统配置的新的预配文件可以包含以下项目：

-   配置文件、 计划说明和使用情况

-   计划说明和使用情况 （更新现有的配置文件）

-   计划使用情况 （更新现有配置文件和计划）

如果将应用新的配置文件和 XML 中未定义的引用计划，预配的结果将包含一条警告。

### <a name="update-data-usage-by-using-an-sms-message"></a>使用短信更新数据使用情况

这是通过以下方式之一来实现：

-   指定运算符消息、 接收运算符通知消息、 通过使用 SMS API，读取该消息在应用中，将消息解析，然后使用设置的用法**IProvisionedProfile**。

-   指定具有有效的使用情况字段组合运算符消息规则，并直接提供的更新后的使用率以短信。

## <a name="span-idtblshtprovspanspan-idtblshtprovspantroubleshooting"></a><span id="tblshtprov"></span><span id="TBLSHTPROV"></span>故障排除


如果您遇到的预配问题，您可以使用下列部分来帮助你找出。

### <a name="span-idprovisioningapiresultsspanspan-idprovisioningapiresultsspanspan-idprovisioningapiresultsspanprovisioning-api-results"></a><span id="Provisioning_API_results"></span><span id="provisioning_api_results"></span><span id="PROVISIONING_API_RESULTS"></span>预配 API 结果

如果预配失败，将收到一个异常，当您尝试执行预配操作。 可能会导致异常的失败包括：

-   预配 XML 不符合[CarrierControlSchema 架构](https://msdn.microsoft.com/library/windows/apps/hh868312)。

-   预配 XML 需要一个签名，但未正确签名。

### <a name="span-idpartialprovisioningfailuresspanspan-idpartialprovisioningfailuresspanspan-idpartialprovisioningfailuresspanpartial-provisioning-failures"></a><span id="Partial_provisioning_failures"></span><span id="partial_provisioning_failures"></span><span id="PARTIAL_PROVISIONING_FAILURES"></span>部分预配失败

预配操作的某些部分可能会因各种原因而失败。 例如，您可能对不存在时的预配的 Wi-fi 硬件的引用。 预配代理执行最大努力以尝试预配该文件中的所有内容。 后出现故障，它将以异步方式返回通过使用在预配结果中记下[ **ProvisionFromXmlDocumentAsync**](https://msdn.microsoft.com/library/windows/apps/br207400)。

结果以 XML 形式返回，并且可以对其进行分析，以发现失败。 元素提供了结构，以显示失败，并**ErrorCode**特性指示作为标准 HRESULT 失败的原因。

例如，以下的错误代码指示由于 WLAN 服务处于不活动状态的预配任何 WLAN 配置文件：

``` syntax
<CarrierProvisioningResult>
    <WLANProfiles ErrorCode=”80070426”/>
</CarrierProvisioningResult>
```

如果无法应用的各个配置文件，则会按如下所示：

``` syntax
<CarrierProvisioningResult>
    <WLANProfiles>
        <WLANProfile Name=”MyProfile” ErrorCode=”80070005”/>
    </WLANProfiles>
</CarrierProvisioningResult>
```

### <a name="span-ideventlogsspanspan-ideventlogsspanspan-ideventlogsspanevent-logs"></a><span id="Event_Logs"></span><span id="event_logs"></span><span id="EVENT_LOGS"></span>事件日志

中的事件**应用程序和服务日志\\Microsoft\\Windows\\NetworkProvisioning\\Operational**通道可以提供有关预配的详细的反馈失败。

### <a name="span-idpowershellprovisioningtesthelpermodulespanspan-idpowershellprovisioningtesthelpermodulespanspan-idpowershellprovisioningtesthelpermodulespanpowershell-provisioningtesthelper-module"></a><span id="PowerShell_ProvisioningTestHelper_module"></span><span id="powershell_provisioningtesthelper_module"></span><span id="POWERSHELL_PROVISIONINGTESTHELPER_MODULE"></span>PowerShell ProvisioningTestHelper 模块

您可以导入**ProvisioningTestHelper**从 Windows 8、 Windows 8.1 和 Windows 10 Sdk 模块。 通过使用此模块，可以生成和安装 EV 证书、 使用的已安装的证书签名的 XML 文件和根据预配的架构验证 XML。 若要将模块导入 PowerShell 会话中，键入以下命令：

``` syntax
Import-Module "<path_to_sdk>\bin\<arch>\ProvisioningTestHelper.psd1"
```

其中&lt;*路径\_到\_sdk\\bin\\&lt;arch&gt;*  &gt;是 Windows 8，Windows 8.1 的安装位置或对应于计算机的体系结构的 Windows 10 SDK。

导入此模块后，即可用以下四个 PowerShell cmdlet:

-   **安装 TestEVCert**生成新的 CA 证书、 将其注册到测试计算机配置为受信任的 EV SSL 提供程序，并使用它来生成和安装使用的 EV 证书的签名。 必须只进行一次运行此 cmdlet，若要安装证书。 可以通过使用证书注册任意数量的文件。

    ``` syntax
    Install-TestEVCert -CertName <Certificate Name> -RootCertOutputPath <complete path to the folder to which the root certificate is to be exported>
    ```

    客户端证书已在命令中指定的名称和根证书的"Root"，以及客户端证书名称追加到它。 *-CertName*参数是可选的。 如果未指定 – CertName 参数， **MBAPTestCert**使用。

    *-RootCertOutputPath*参数也是可选的。 如果你想要导出的根证书安装在另一台计算机上使用安装 RootCertFromFile cmdlet 应使用它。

-   **安装 RootCertFromFile**适用测试根证书的不同计算机上，若要测试的开发计算机之外的计算机上的客户端体验。

    ``` syntax
    Install-RootCertFromFile -CertFile <complete path to the root certificate>
    ```

-   **ConvertTo SignedXml**使用 EV 证书 （对于测试，生成或由第三方提供商发行） 将 XML DSig 签名应用于的置备 XML 文件。 此签名从受信任的证书将导致 Windows 以接受来自任何关联硬件，移动宽带应用有效的预配文件。

    ``` syntax
    ConvertTo-SignedXml -InputFile <complete path to the input XML file> -OutputFile <complete path to the output XML file> -CertName <name of the certificate used to sign the xml>
    ```

    此命令将输入的 XML 文件进行签名、 签名放在 XML 中，并将其保存到输出 XML 文件。

-   **测试 ValidProvisioningXml**针对预配的架构验证预配 XML （带符号或无符号）。

    ``` syntax
    Test-ValidProvisioningXml -InputFile <complete path to the input XML file>
    ```

 

 





