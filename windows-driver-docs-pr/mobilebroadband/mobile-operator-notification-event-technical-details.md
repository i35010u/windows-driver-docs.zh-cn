---
title: 移动运营商通知事件技术详细信息
description: 移动运营商通知事件技术详细信息
ms.assetid: 639f238a-4bb4-4ac0-9b59-92a761dbc351
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e25284f32fe27ffdd4379ec3c218045d1a7ad708
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356927"
---
# <a name="mobile-operator-notification-event-technical-details"></a>移动运营商通知事件技术详细信息


本主题说明移动运营商通知事件的技术详细信息。

-   [事件负载](#eventpl)

-   [通过使用元数据注册 MobileOperatorNotification 事件](#regmd)

-   [在预配 XML 中定义的筛选规则](#deffilter)

## <a name="span-ideventplspanspan-ideventplspanevent-payload"></a><span id="eventpl"></span><span id="EVENTPL"></span>事件负载


MobileOperatorNotification 事件有效负载包括以下字段：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>字段</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MessageType</strong></p></td>
<td><p>触发事件的消息的枚举。</p></td>
</tr>
<tr class="even">
<td><p><strong>Interface</strong></p></td>
<td><p>对应于与事件相关联的物理接口的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EncodingType</strong></p></td>
<td><p>如果编码方法的消息<strong>MessageType</strong>是 SMS/USSD。</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageDataSize</strong></p></td>
<td><p>大小的消息，以字节为单位，如果<strong>MessageType</strong>是 SMS/USSD。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Message</strong></p></td>
<td><p>收到时，如果原始消息<strong>MessageType</strong>是 SMS/USSD。</p></td>
</tr>
</tbody>
</table>

 

MobileOperatorNotification 事件，每个方案中所述[移动运营商通知方案](mobile-operator-notification-scenarios.md)加以区分使用**MessageType**事件中字段有效负载。 **MessageType**s 枚举，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>枚举</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>GSM SMS</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>CDMA SMS</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>USSD</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>DataPlanThresholdReached</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>DataPlanReset</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>DataPlanDeleted</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p>ProfileConnected</p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>ProfileDisconnected</p></td>
</tr>
<tr class="odd">
<td><p>8</p></td>
<td><p>RegisteredRoaming</p></td>
</tr>
<tr class="even">
<td><p>9</p></td>
<td><p>RegisteredHome</p></td>
</tr>
<tr class="odd">
<td><p>10</p></td>
<td><p>TetheringEntitlementCheck</p></td>
</tr>
</tbody>
</table>

 

与 MobileOperatorNotification 事件相关联的工作项应以有效地区分的逻辑开头**MessageType**，并运行每个方案的相应代码。

### <a name="span-idgsmetcspanspan-idgsmetcspangsmcdma-sms-and-ussd"></a><span id="gsmetc"></span><span id="GSMETC"></span>GSM/CDMA SMS 和 USSD

传入运算符消息，包括短信和 USSD，触发 MobileOperatorNotification 事件与适当的对应**MessageType**s。 这些类型的特有功能都**EncodingType**， **MessageDataSize**，并**消息**。

### <a name="span-iddataplanthresholdreachedspanspan-iddataplanthresholdreachedspanspan-iddataplanthresholdreachedspandataplanthresholdreached"></a><span id="DataPlanThresholdReached"></span><span id="dataplanthresholdreached"></span><span id="DATAPLANTHRESHOLDREACHED"></span>DataPlanThresholdReached

默认情况下，禁用此消息类型。 你可以通过使用预配的元数据指定启用它[ **DataUsageInMobileOperatorNotificationEnabled** ](https://msdn.microsoft.com/library/windows/apps/hh868368)字段，如下所示。

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

帐户预配的元数据的详细信息，请参阅[帐户预配](account-provisioning.md)。

与此生成事件**MessageType**移动宽带接口上的本地数据计数器时估计使用情况 （发送和接收字节） 5%自以来已更改最后一个匹配项，除在以下情况下：

1.  当连接到家庭网络 （非漫游），如果尚未指定数据的计划限制，则触发此事件在每个 100 MB 的本地数据使用情况。

2.  连接到漫游网络时，数据计划限制不适用，并且在每个 5 MB 的本地数据使用情况触发此事件。

在 Windows 8 中的本地数据计数器会更新每分钟一次;最多，生成此事件是每分钟在所有方案中所述的一次。 在 Windows 8.1 中时实时发送事件已达到 5%阈值。

**请注意**  尽管此信息是一个很好的一级，Windows 无法解释为未出单流量，或者使用共享 （如系列计划或 SIM 交换） 相同的数据限制其他设备上。 移动运营商应用程序应使用本地数据计数器仅以操作员的计费系统与在上次同步后估计使用情况。 对于已处理的数据使用情况，计费系统应将视为权威标准。

 

### <a name="span-iddataplanresetspanspan-iddataplanresetspanspan-iddataplanresetspandataplanreset"></a><span id="DataPlanReset"></span><span id="dataplanreset"></span><span id="DATAPLANRESET"></span>DataPlanReset

计划重置日期后，数据使用情况和订阅管理器 (DUSM) 重置用户的当前本地数据使用情况为零。

### <a name="span-iddataplandeletedspanspan-iddataplandeletedspanspan-iddataplandeletedspandataplandeleted"></a><span id="DataPlanDeleted"></span><span id="dataplandeleted"></span><span id="DATAPLANDELETED"></span>DataPlanDeleted

对于有固定的到期日期的预先付费的数据计划，DUSM 删除到期日期是与帐户关联的连接配置文件，并通过使用此触发 MobileOperatorNotification 事件**MessageType**. 删除连接配置文件时，Windows 连接管理器不再尝试自动连接到网络的连接配置文件描述。

### <a name="span-idprofileconnectedandprofiledisconnectedspanspan-idprofileconnectedandprofiledisconnectedspanspan-idprofileconnectedandprofiledisconnectedspanprofileconnected-and-profiledisconnected"></a><span id="ProfileConnected_and_ProfileDisconnected"></span><span id="profileconnected_and_profiledisconnected"></span><span id="PROFILECONNECTED_AND_PROFILEDISCONNECTED"></span>ProfileConnected 和 ProfileDisconnected

MobileOperatorNotification 事件生成具有这些**MessageType**s Windows 连接管理器连接到提供的运营商体验元数据的网络配置文件时。 此事件在每个连接时触发，断开连接，包括遵循睡眠/恢复的初始连接。 它也会触发如果设备已连接时下载和安装应用程序和服务元数据。

在移动宽带接口的 L2 连接时触发 ProfileConnected MessageType。

**请注意**  网络标识完成之前，将发生此触发器。 [ **NetworkStatusChanged** ](https://msdn.microsoft.com/library/windows/apps/br207299)事件 (属于[ **NetworkInformation** ](https://msdn.microsoft.com/library/windows/apps/br207293) API) 生成时的网络标识确定网络的连接级别。 有关网络标识的详细信息，请参阅[快速入门：检索网络连接信息](https://msdn.microsoft.com/library/windows/apps/hh452990)并**NetworkInformation**类。

 

### <a name="span-idregisteredroamingandregisteredhomespanspan-idregisteredroamingandregisteredhomespanspan-idregisteredroamingandregisteredhomespanregisteredroaming-and-registeredhome"></a><span id="RegisteredRoaming_and_RegisteredHome"></span><span id="registeredroaming_and_registeredhome"></span><span id="REGISTEREDROAMING_AND_REGISTEREDHOME"></span>RegisteredRoaming 和 RegisteredHome

MobileOperatorNotification 事件生成具有这些**MessageType**当 Windows 连接管理器将会注册到漫游网络时。 每个注册，包括初始注册后睡眠/恢复上触发此事件。 如果设备已注册到网络时下载和安装应用程序和服务元数据，它还会触发。

应用程序应仅通知用户漫游网络注册时的一次，一次当用户返回到其家庭网络。 因为在每个注册时会触发此事件，则应用负责跟踪的应用程序的会话数据中的上一个已注册的状态。

### <a name="span-idtetheringentitlementcheckspanspan-idtetheringentitlementcheckspanspan-idtetheringentitlementcheckspantetheringentitlementcheck"></a><span id="TetheringEntitlementCheck"></span><span id="tetheringentitlementcheck"></span><span id="TETHERINGENTITLEMENTCHECK"></span>TetheringEntitlementCheck

MobileOperatorNotification 事件生成与此**MessageType**的用户打开时 Internet 共享。 每次用户尝试使用 Internet 共享，只要移动运营商已设置时，都会触发该事件[AllowTethering](allowtethering.md)服务元数据架构中的元素**EntitlementCheckRequired**。 有关服务的元数据架构的详细信息，请参阅[服务的元数据数据包架构参考](service-metadata-package-schema-reference.md)。

应用应运行支持的移动运营商网络的相应权利检查机制并将结果发送到系统中，通过使用[ **AuthorizeTethering** ](https://msdn.microsoft.com/library/windows/apps/dn266090)方法[ **NetworkOperatorNotificationEventDetails** ](https://msdn.microsoft.com/library/windows/apps/br207377)类[ **Windows.Networking.NetworkOperators** ](https://msdn.microsoft.com/library/windows/apps/br241148)命名空间。 如果应用不具有运行权利检查的功能，移动运营商应更改服务元数据[AllowTethering](allowtethering.md)元素**始终**或**从不**，以便永远不会生成事件。

## <a name="span-idregmdspanspan-idregmdspanregister-for-the-mobileoperatornotification-event-by-using-metadata"></a><span id="regmd"></span><span id="REGMD"></span>通过使用元数据注册 MobileOperatorNotification 事件


一般情况下，应用必须由用户运行之前它可以向系统事件代理注册的工作项的至少一次。 但是，因为完成密钥的移动宽带方案所需的 MobileOperatorNotification 事件，此事件是与移动宽带应用关联通过使用服务元数据。 在服务元数据，配置[DeviceCompanionApplications](devicecompanionapplications.md)元素。

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

**EventID**属性通知系统的哪种设备时会出现的情况的事件。 值**EventAsset**属性应指向实现后台任务的入口点。 这将告知系统要运行该特定事件发生时的任务。

使用此示例中，系统将创建并注册特定于该设备的事件。 它还会注册此事件的移动宽带应用。 应用程序必须具有一个名为 backgroundtask.js 是由系统每次运行它收到的操作员通知的 JavaScript 文件。

如果移动宽带应用以C#，事件资产必须指向实现 backgroundtask 接口的运行时类。

``` syntax
<DeviceNotificationHandlers>
  <DeviceNotificationHandler EventID="MobileOperatorNotificationHandler" EventAsset="MNOMessageBackground.OperatorNotification" />
```

服务元数据和应用程序在下载时，设备安装程序管理器之前运行该应用注册相应的工作项与系统事件代理。 立即注册工作项，如果移动宽带设备是注册，或者连接到网络后，将 MobileOperatorNotification 事件触发与相应**MessageType**。

### <a name="span-idchangebackgroundtaskregistrationinmetadataspanspan-idchangebackgroundtaskregistrationinmetadataspanspan-idchangebackgroundtaskregistrationinmetadataspanchange-background-task-registration-in-metadata"></a><span id="Change_background_task_registration_in_metadata"></span><span id="change_background_task_registration_in_metadata"></span><span id="CHANGE_BACKGROUND_TASK_REGISTRATION_IN_METADATA"></span>更改元数据中的后台任务注册

如果在移动宽带的应用程序的更新版本中更改的后台任务入口点[DeviceNotificationHandler](devicenotificationhandler.md)也必须更改服务元数据中的元素。

运行 Windows 8、 Windows 8.1 和 Windows 10 的计算机上自动更新服务元数据。 移动宽带应用程序会在 Microsoft Store 中更新。 应避免更改[DeviceNotificationHandler](devicenotificationhandler.md)后台服务元数据中的任务注册。 如果需要更改，服务元数据应包含对所有不同的背景任务入口点使用所有的移动宽带应用程序的受支持版本中保留的用户未更新移动宽带功能的引用应用程序。

## <a name="span-iddeffilterspanspan-iddeffilterspandefine-filtering-rules-in-provisioning-xml"></a><span id="deffilter"></span><span id="DEFFILTER"></span>在预配 XML 中定义的筛选规则


Windows 接受你的基于 XML 的预配文件。 置备 XML 的示例版本如下所示：

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

帐户预配的元数据的详细信息，请参阅[帐户预配](account-provisioning.md)。

要识别的短信，可以在此 XML 中定义的运算符消息的规则。

-   **允许发件人**发件人属性指定该通知允许到达保留发件人地址。 （此数字必须完全符合接收 SMS 消息，包括国际格式中的发件人号）。

-   **模式**正则表达式以标识和 （可选） 的文本消息中提取数据字段。 若要匹配所有消息从发送方，使用模式`[^]*`。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)

[创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)

 

 






