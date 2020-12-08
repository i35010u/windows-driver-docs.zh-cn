---
title: 移动运营商通知方案
description: 移动运营商通知方案
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69a4cd5a95d3bd3eb1499e111dbdb856ec2ea9a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840321"
---
# <a name="mobile-operator-notification-scenarios"></a>移动运营商通知方案


本主题介绍在移动宽带应用中使用移动运营商通知时的情况。

-   [连接并断开与移动宽带的连接](#conndis)

-   [网络操作员消息](#netopmsg)

-   [在本地触发数据使用和漫游通知](#trigloc)

-   [数据计划过期和使用重置](#expire)

-   [Internet 共享的权利检查](#sharing)

## <a name="span-idconndisspanspan-idconndisspanconnect-to-and-disconnect-from-mobile-broadband"></a><span id="conndis"></span><span id="CONNDIS"></span>连接并断开与移动宽带的连接


Windows 连接管理器跨 Wi-fi、移动宽带和以太网监视可用网络。 它基于可用网络进行自动连接和断开连接决策。 当 Windows 连接管理器连接到移动宽带配置文件并断开与它的连接时，将触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 的后台事件。 当用户连接到其网络（如验证帐户状态、检索最新的数据使用情况，或显示通知和磁贴更新）时，此事件使移动宽带应用可以执行必要的逻辑。

## <a name="span-idnetopmsgspanspan-idnetopmsgspannetwork-operator-messages"></a><span id="netopmsg"></span><span id="NETOPMSG"></span>网络操作员消息


Windows 8 中的移动宽带平台 Windows 8.1 和 Windows 10 提供了仅适用于移动宽带应用的增强功能，用于接收和显示传入的 SMS 和 USSD 管理消息。 这些消息可用于用户通知，如接近数据使用量上限、国际漫游、低余额，或者触发移动宽带应用的响应。

应用根据需要处理传入消息。 可能的响应包括以下任何一项或所有项：

-   立即同步当前数据使用情况

-   更新移动宽带应用的磁贴

-   检索和应用更新的操作员预配 XML

-   向用户显示通知

如果要在应用程序中显示消息， [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件触发的后台任务必须读取消息内容，并将消息内容存储在应用自己的本地数据存储中。 移动宽带 SMS 平台不维护收到的管理 SMS 通知队列。

### <a name="span-idmobile_network_operator_sms_notificationsspanspan-idmobile_network_operator_sms_notificationsspanspan-idmobile_network_operator_sms_notificationsspanmobile-network-operator-sms-notifications"></a><span id="Mobile_network_operator_SMS_notifications"></span><span id="mobile_network_operator_sms_notifications"></span><span id="MOBILE_NETWORK_OPERATOR_SMS_NOTIFICATIONS"></span>移动网络操作员 SMS 通知

传入的 SMS 消息可用于已请求并被授予计算机上 SMS 功能访问权限的任何应用。 但是，某些 SMS 消息直接来自载波，并应限制为移动宽带应用程序并进行处理。

移动宽带 SMS 平台将每个新收到的短信筛选为以下两种类型之一：管理 (从移动网络运营商处) SMS 通知 (o) 和一般 SMS 消息。 从 o 接收的管理短信通知只能访问移动宽带应用，并且不会从常规 SMS 客户端应用中隐藏。

Mno 在帐户预配元数据中为管理 SMS 和 USSD 通知指定自定义筛选规则。 如果未指定消息筛选规则，则 SMS 平台会将所有 SMS 消息分类为适用于任何应用程序的常规 SMS 消息。 如果传入的 SMS 与预配的筛选规则匹配，则会触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件，并且后台工作项可以处理传入的 sms 消息。

### <a name="span-idnetwork-initiated_ussdspanspan-idnetwork-initiated_ussdspanspan-idnetwork-initiated_ussdspannetwork-initiated-ussd"></a><span id="Network-initiated_USSD"></span><span id="network-initiated_ussd"></span><span id="NETWORK-INITIATED_USSD"></span>网络启动的 USSD

Windows 8、Windows 8.1 和 Windows 10 提供 USSD API，该 API 是底层 USSD 协议的抽象，可隐藏大部分细节来简化应用程序开发。 接收到与预配筛选规则匹配的网络启动的 USSD 时， [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件为触发，相应的后台工作项可以通过使用 USSD API 通过 USSD 会话进行通信。

有关 USSD Api 的详细信息，请参阅 [**windows.networking.networkoperators**](/uwp/api/Windows.Networking.NetworkOperators) 命名空间。

## <a name="span-idtriglocspanspan-idtriglocspantriggering-data-usage-and-roaming-notifications"></a><span id="trigloc"></span><span id="TRIGLOC"></span>触发数据使用情况和漫游通知


在许多方面，监管法要求 Mno 在用户达到其数据使用限制时通知用户，或在更昂贵的网络上漫游。 此使用者保护降低了过度使用费用的风险。 在 Windows 中，移动宽带应用可以显示 toast 通知和磁贴更新，以使用户了解数据使用情况和漫游状态。 可以通过使用 SMS 或 USSD （触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件）从网络后端启动这些通知。 或者，在以下情况下，可以使用本地信息触发 MobileOperatorNotification 事件。

### <a name="span-iddata_usage_notification_by_using_local_data_countersspanspan-iddata_usage_notification_by_using_local_data_countersspanspan-iddata_usage_notification_by_using_local_data_countersspandata-usage-notification-by-using-local-data-counters"></a><span id="Data_usage_notification_by_using_local_data_counters"></span><span id="data_usage_notification_by_using_local_data_counters"></span><span id="DATA_USAGE_NOTIFICATION_BY_USING_LOCAL_DATA_COUNTERS"></span>使用本地数据计数器的数据使用通知

1.  可以通过使用预配元数据启用本地数据使用通知。

2.  本地数据计数器估计，自上次更新以来，配置文件上的使用情况已更改，超过用户数据限制的5%。

3.  数据使用情况和订阅管理器 (DUSM) 通知系统事件代理触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件。

4.  系统事件代理调用移动宽带应用程序来处理后台事件。

5.  此应用通过从后端基础结构检索最新的使用情况信息来处理事件。

6.  如果当前使用情况信息超过阈值 (例如 80% ) ，则应用会向用户显示 toast 通知，并使用当前使用情况更新 DUSM。 或者，如果当前使用量不超过阈值，则应用无需显示 toast 通知。

### <a name="span-idroaming_notification_by_using_windows_connection_managerspanspan-idroaming_notification_by_using_windows_connection_managerspanspan-idroaming_notification_by_using_windows_connection_managerspanroaming-notification-by-using-windows-connection-manager"></a><span id="Roaming_notification_by_using_Windows_Connection_Manager"></span><span id="roaming_notification_by_using_windows_connection_manager"></span><span id="ROAMING_NOTIFICATION_BY_USING_WINDOWS_CONNECTION_MANAGER"></span>使用 Windows 连接管理器的漫游通知

1.  Windows 连接管理器注册在漫游移动宽带网络上。

2.  Windows 连接管理器通知系统事件代理触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件。

3.  系统事件代理调用移动运营商应用程序来处理后台事件。

4.  此应用在此网络上漫游时确定用户是否会产生额外的使用费用，如有必要，将显示 toast 通知并将更新磁贴到用户。

## <a name="span-idexpirespanspan-idexpirespandata-plan-expiration-and-usage-reset"></a><span id="expire"></span><span id="EXPIRE"></span>数据计划过期和使用重置


DUSM 跟踪有关用户帐户的详细信息，包括预先支付的数据计划的计划到期日期或支付后的数据计划的计划使用情况重置日期。 当用户的数据计划过期时，DUSM 将通知系统事件代理触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件。 移动宽带应用可以通过向用户显示 toast 通知和磁贴更新来处理事件，通知他们计划已过期或指导他们续订其服务。

对于已支付后的数据计划，DUSM 会将计划数据使用情况从特定日期重置为零，如月份的第一天。 出现这种情况时，将触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件，应用可以通知用户其更新的数据使用情况。

## <a name="span-idsharingspanspan-idsharingspanentitlement-check-for-internet-sharing"></a><span id="sharing"></span><span id="SHARING"></span>Internet 共享的权利检查


在 Windows 8.1 中，已添加 Internet 共享（通常称为 tethering），以使用户能够与不支持移动宽带功能的一个或多个其他设备共享其移动宽带网络连接。 传统的 tethering 机制包括蓝牙和 USB。 不过，Wi-Fi 可以提供快速轻松的移动宽带连接共享机制（如个人热点、移动热点等），因为它需要较少的配置、支持高速数据传输，并依赖于熟悉的 Wi-Fi 连接过程。

某些 Mno 或 Mvno 在其网络上不支持 Internet 共享功能，或者在设置 Internet 共享连接之前需要进行权利检查。 Windows 提供必要的控件，以确保 Windows 设备符合网络策略。 如果移动运营商已在服务元数据包中将 [AllowTethering](allowtethering.md) 元素设置为 **EntitlementCheckRequired** ，则系统将触发 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md) 事件。 然后，移动宽带应用与网络服务通信，以检查是否允许用户使用 Internet 共享功能并响应系统。 如果允许用户使用此功能，则 Internet 共享将成功启动，否则，将显示默认错误消息或移动运营商定义的消息。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)

[创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)

 

