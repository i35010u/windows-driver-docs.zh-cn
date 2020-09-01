---
title: 移动运营商通知事件技术详细信息
description: 移动运营商通知事件技术详细信息
ms.assetid: 639f238a-4bb4-4ac0-9b59-92a761dbc351
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c989b43146b4594a32dc3989778881254da2042
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212559"
---
# <a name="mobile-operator-notification-event-technical-details"></a>移动运营商通知事件技术详细信息

本主题介绍移动运营商通知事件的技术详细信息。

- [事件负载](#event-payload)

- [使用元数据注册 MobileOperatorNotification 事件](#register-for-the-mobileoperatornotification-event-by-using-metadata)

- [在预配 XML 中定义筛选规则](#define-filtering-rules-in-provisioning-xml)

## <a name="event-payload"></a>事件负载

MobileOperatorNotification 事件负载包括以下字段：

|字段|说明|
|----|----|
|**MessageType**|触发事件的消息的枚举。|
|**Interface**|与事件关联的物理接口对应的 GUID。|
|**EncodingType**|如果 **MessageType** 为 SMS/USSD，则为消息编码方法。|
|**MessageDataSize**|如果 **MessageType** 为 SMS/USSD，则为消息大小（以字节为单位）。|
|**消息**|如果 **MessageType** 为 SMS/USSD，则接收到的原始消息。|

MobileOperatorNotification 事件通过使用事件负载中的**MessageType**字段，来区分[移动运营商通知方案](mobile-operator-notification-scenarios.md)中描述的每个方案。 **MessageType**的枚举如下：

|枚举|类型|
|----|----|
|0|GSM 短信|
|1|CDMA 短信|
|2|USSD|
|3|DataPlanThresholdReached|
|4|DataPlanReset|
|5|DataPlanDeleted|
|6|ProfileConnected|
|7|ProfileDisconnected|
|8|RegisteredRoaming|
|9|RegisteredHome|
|10|TetheringEntitlementCheck|

与 MobileOperatorNotification 事件相关联的工作项应以有效区分 **MessageType**的逻辑开始，并为每个方案运行相应的代码。

### <a name="gsmcdma-sms-and-ussd"></a>GSM/CDMA 短信和 USSD

传入的操作员消息（包括短信和 USSD）将触发 MobileOperatorNotification 事件以及相应的 **MessageType**。 这些类型的独特之处是 **EncodingType**、 **MessageDataSize**和 **Message**。

### <a name="dataplanthresholdreached"></a>DataPlanThresholdReached

默认情况下，此消息类型处于禁用状态。 可以通过使用预配元数据指定 [**DataUsageInMobileOperatorNotificationEnabled**](/uwp/schemas/mobilebroadbandschema/plans/element-datausageinmobileoperatornotificationenabled) 字段来启用此功能，如下所示。

``` syntax
<?xml version="1.0"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
  <Global>
    <CarrierId>{2c85b76b-f859-47c4-8122-721fe8b6c25f}</CarrierId>
    <SubscriberId>012345678901234</SubscriberId>
  </Global>
  <MBNProfiles>
    <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
      <Name>Contoso</Name>
      <AssociatedPlan>SamplePlan</AssociatedPlan>
      <Context>
        <AccessString>Contoso.com</AccessString>
        <UserLogonCred>
          <UserName>User</UserName>
          <Password>pass</Password>
        </UserLogonCred>
      </Context>
    </DefaultProfile>
  </MBNProfiles>
  <Plans>
    <Plan xmlns="http://www.microsoft.com/networking/CarrierControl/Plans/v1" Name="SamplePlan">
      <Description PlanType="Fixed">
        <DataLimitInMegabytes>500</DataLimitInMegabytes>
        <DataUsageInMobileOperatorNotificationEnabled>true</DataUsageInMobileOperatorNotificationEnabled>
      </Description>
    </Plan>
  </Plans>
</CarrierProvisioning>
```

有关帐户预配元数据的详细信息，请参阅 [帐户预配](account-provisioning.md)。

如果本地数据计数器预计在移动宽带接口上发送和接收的字节数 (在移动宽带接口上发送和) 接收的字节数在上次发生后5% 发生了更改（在以下情况下除外），则将使用此 **MessageType** 生成事件：

1. 当连接到家庭网络 (非漫游) 时，如果尚未指定数据计划限制，则将每隔 100 MB 的本地数据使用触发此事件。

2. 连接到漫游网络后，数据计划限制不适用，并且每隔 5 MB 的本地数据会触发此事件。

Windows 8 中的本地数据计数器每分钟更新一次;在所有描述的方案中，此事件最多每分钟生成一次。 在 Windows 8.1 达到5% 阈值时，会实时传递事件。

>[!NOTE]
>尽管此信息是一个不错的第一本指南，但 Windows 无法在共享相同数据限制 (例如系列计划或 SIM 交换) 的其他设备上考虑未开票流量或使用情况。 移动运营商应用只应使用本地数据计数器来估算自上次同步到操作员自己的计费系统后的使用量。 对于已处理的数据使用，计费系统应视为权威系统。

### <a name="dataplanreset"></a>DataPlanReset

在计划重置日期，数据使用量和订阅管理器 (DUSM) 将用户的当前本地数据使用量重置为零。

### <a name="dataplandeleted"></a>DataPlanDeleted

对于具有固定到期日期的预先支付的数据计划，DUSM 会删除与帐户相关联的到期日期的连接配置文件，并使用此 **MessageType**触发 MobileOperatorNotification 事件。 当连接配置文件被删除后，Windows 连接管理器不再尝试自动连接到连接配置文件描述的网络。

### <a name="profileconnected-and-profiledisconnected"></a>ProfileConnected 和 ProfileDisconnected

当 Windows 连接管理器连接到由操作员体验元数据提供的网络配置文件时，将使用这些 **MessageType**生成 MobileOperatorNotification 事件。 此事件在每次连接和断开连接时触发，包括睡眠/恢复之后的初始连接。 如果在下载和安装应用和服务元数据时设备已连接，也会触发此情况。

ProfileConnected MessageType 在移动宽带接口的 L2 连接上触发。

>[!NOTE]
>此触发器在网络标识完成之前发生。 当网络标识确定网络的连接级别时，将生成[**System.net.networkinformation**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation) API)  (部分的[**NetworkStatusChanged**](/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged)事件。 有关网络标识的详细信息，请参阅 [快速入门：检索网络连接信息](/previous-versions/windows/apps/hh452990(v=win.10)) 和 **system.net.networkinformation** 类。

### <a name="registeredroaming-and-registeredhome"></a>RegisteredRoaming 和 RegisteredHome

当 Windows 连接管理器注册到漫游网络时，将使用这些 **MessageType**生成 MobileOperatorNotification 事件。 此事件在每次注册时触发，包括在睡眠/恢复之后初始注册。 如果在下载和安装应用和服务元数据时，设备已注册到网络，也会触发此情况。

应用只应在用户注册漫游网络时通知用户一次，并在其返回到家庭网络时通知用户。 由于此事件在每次注册时触发，因此应用负责跟踪应用会话数据中以前注册的状态。

### <a name="tetheringentitlementcheck"></a>TetheringEntitlementCheck

当用户开启 Internet 共享时，将生成带有此 **MessageType**的 MobileOperatorNotification 事件。 只要移动运营商已将服务元数据架构中的 [AllowTethering](allowtethering.md) 元素设置为 **EntitlementCheckRequired**，就会在用户每次尝试使用 Internet 共享时触发事件。 有关服务元数据架构的详细信息，请参阅 [服务元数据包架构参考](mobilebroadbandinfo-xml-schema.md)。

应用应运行移动运营商网络支持的适当的权限检查机制，并使用[**NetworkOperatorNotificationEventDetails**](/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails)类的[**AuthorizeTethering**](/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails#Windows_Networking_NetworkOperators_NetworkOperatorNotificationEventDetails_AuthorizeTethering_System_Boolean_System_String_)方法将结果发送到[**系统。**](/uwp/api/Windows.Networking.NetworkOperators) 如果应用无法运行权利检查，则移动运营商应将服务元数据 [AllowTethering](allowtethering.md) 元素更改为 **Always** 或 **never**，以便永远不会生成该事件。

## <a name="register-for-the-mobileoperatornotification-event-by-using-metadata"></a>使用元数据注册 MobileOperatorNotification 事件

通常，应用必须至少运行一次，然后才能将工作项注册到系统事件代理。 不过，由于需要 MobileOperatorNotification 事件来完成关键移动宽带方案，因此此事件通过使用服务元数据与移动宽带应用相关联。 在服务元数据中，配置 [DeviceCompanionApplications](devicecompanionapplications.md) 元素。

``` syntax
<DeviceCompanionApplications>
  <Package>
    <Identity Name="MyOperatorNotification" Publisher="MyCorporation " />
    <Applications>
      <Application Id="MyOperatorNotification" />
        <DeviceNotificationHandlers>
          <DeviceNotificationHandler EventID="MobileOperatorNotificationHandler" EventAsset="backgroundtask.js" />
      </DeviceNotificationHandlers>
    </Applications>
  </Package>
</DeviceCompanionApplications>
```

**EventID**特性告诉系统要从设备获得的事件类型。 **EventAsset**属性的值应指向实现后台任务的入口点。 这会告知系统当发生特定事件时要运行的任务。

使用此示例，系统创建并注册特定于该设备的事件。 它还为此事件注册移动宽带应用。 应用必须具有名为 backgroundtask.js 的 JavaScript 文件，该文件在每次收到操作员通知时由系统运行。

如果移动宽带应用是用 c # 编写的，则事件资产必须指向实现 backgroundtask 接口的运行时类。

``` syntax
<DeviceNotificationHandlers>
  <DeviceNotificationHandler EventID="MobileOperatorNotificationHandler" EventAsset="MNOMessageBackground.OperatorNotification" />
```

下载服务元数据和应用时，设备安装管理器会在运行应用之前向系统事件代理注册相应的工作项。 注册工作项后，如果移动宽带设备已注册或连接到网络，则会立即触发 MobileOperatorNotification 事件和相应的 **MessageType**。

### <a name="change-background-task-registration-in-metadata"></a>在元数据中更改后台任务注册

如果在移动宽带应用的更新版本中更改了后台任务入口点，则还必须更改服务元数据中的 [DeviceNotificationHandler](devicenotificationhandler.md) 元素。

服务元数据在运行 Windows 8、Windows 8.1 和 Windows 10 的计算机上自动更新。 移动宽带应用在 Microsoft Store 中进行了更新。 应避免更改服务元数据中的 [DeviceNotificationHandler](devicenotificationhandler.md) 后台任务注册。 如果需要进行更改，服务元数据应包含对所有支持的移动宽带应用程序版本中使用的所有不同后台任务入口点的引用，以保留尚未更新移动宽带应用的用户的功能。

## <a name="define-filtering-rules-in-provisioning-xml"></a>在预配 XML 中定义筛选规则

Windows 接受来自基于 XML 的预配文件。 设置 XML 的示例版本如下所示：

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<CarrierProvisioning xmlns="http://www.microsoft.com/networking/CarrierControl/v1">
    <Global>
        <!-- Adjust the Carrier ID to fit match the Service Number in service metadata. Refer to the documentation about CarrierId. -->
        <CarrierId>{11111111-1111-1111-1111-111111111111}</CarrierId>
        <!-- Adjust the Susbscriber ID. Refer to the documentation about Subscriber ID's. -->
        <SubscriberId>1234567890</SubscriberId>
    </Global>
    <MBNProfiles>
        <DefaultProfile xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
            <!-- Adjust the profile name -->
            <Name>Contoso</Name>
          <AssociatedPlan>Limited</AssociatedPlan>
            <!-- Adjust the home provider name for the given SIM/Device -->
            <HomeProviderName>Contoso</HomeProviderName>
            <Context>
                <!-- Adjust the access string to your APN. -->
                <AccessString>Contoso.Contoso</AccessString>
                <!-- Adjust the UserLogonCred to fit your UserLogonCred. Refer to the documentation about UserLogonCred's. -->
                <UserLogonCred>
                    <UserName>user</UserName>
                    <Password>password</Password>
                </UserLogonCred>
            </Context>
        </DefaultProfile>
      <Messages xmlns="http://www.microsoft.com/networking/CarrierControl/WWAN/v1">
        <Message RuleId="Sample1" Silent="true">
          <SMSBearer ClassZeroOnly="false" Sender="18005551212"/>
          <!-- [^]* matches all messages from this sender, regardless of content -->
          <Pattern>[^]*</Pattern>
          <!-- Because no Fields are specified, this message will be passed to the operator app without parsing. -->
        </Message>
        <Message RuleId="Sample2" Silent="false">
          <!-- Parsing a simple usage message. -->
          <USSDBearer/>
          <Pattern>(\d+\.\d+)(\w+) of (\d+)(\w+) used as of (\S+)</Pattern>
          <!-- Using these field definitions, Windows will automatically update usage data before passing the message
               to the operator app. -->
          <Units G="GB" M="MB"/>
          <Fields>
            <!-- These fields are currently unordered, but an order will be required in RC. -->
            <Usage Group="1" UnitGroup="2"/>
            <UsageTimestamp Group="5" Format="%I:%M%p on %d %b"/>
            <DataLimit Group="3" UnitGroup="4"/>
          </Fields>
        </Message>
      </Messages>
  </MBNProfiles>
  <Provisioning />
</CarrierProvisioning>
```

有关帐户预配元数据的详细信息，请参阅 [帐户预配](account-provisioning.md)。

可在此 XML 中定义用于将文本消息标识为操作员消息的规则。

- **允许的发送方** Sender 属性指定允许通知到达的保留发送方地址。  (此数字必须与 SMS 消息中收到的发送方号码完全匹配，包括国际格式) 。

- **模式** 用于标识并选择性地从文本消息中提取数据字段的正则表达式。 若要匹配发送方的所有消息，请使用模式 `[^]*` 。

## <a name="related-topics"></a>相关主题

[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)

[创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)