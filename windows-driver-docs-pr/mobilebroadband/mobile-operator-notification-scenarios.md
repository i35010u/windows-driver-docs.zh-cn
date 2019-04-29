---
title: 移动运营商通知方案
description: 移动运营商通知方案
ms.assetid: 3749d9ab-3dff-4216-a23b-0e75c04d9a22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e3f15beb3013c2628437c57a1c38464a75a1d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391972"
---
# <a name="mobile-operator-notification-scenarios"></a>移动运营商通知方案


本主题介绍的方案需要使用移动运营商通知用于移动宽带应用。

-   [连接到并断开与移动宽带连接](#conndis)

-   [网络运算符消息](#netopmsg)

-   [触发数据使用情况和漫游通知保存到本地](#trigloc)

-   [数据计划过期时间和使用情况重置](#expire)

-   [权利检查 Internet 共享](#sharing)

## <a name="span-idconndisspanspan-idconndisspanconnect-to-and-disconnect-from-mobile-broadband"></a><span id="conndis"></span><span id="CONNDIS"></span>连接到并断开与移动宽带连接


Windows 连接管理器监视 Wi-fi、 移动宽带和以太网之间的可用网络。 它可以自动连接和断开决策基于可用的网络。 当 Windows 连接管理器连接到和从移动宽带配置文件，将断开连接时[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)触发后台事件。 此事件，来执行必要的逻辑，当用户连接到网络，例如验证帐户状态、 检索的最新的数据使用情况，或显示通知和磁贴更新的移动宽带应用。

## <a name="span-idnetopmsgspanspan-idnetopmsgspannetwork-operator-messages"></a><span id="netopmsg"></span><span id="NETOPMSG"></span>网络运算符消息


Windows 8、 Windows 8.1 和 Windows 10 中的移动宽带平台提供了增强的功能，可向移动宽带应用，用于接收和显示传入短信和 USSD 管理消息。 这些消息可用于用户通知中，如接近数据使用限制、 国际漫游、 余额偏低，或触发您的移动宽带应用中的响应。

应用程序处理根据传入的消息。 可能响应包括以下的任意或全部：

-   立即同步当前数据使用情况

-   更新移动宽带应用的磁贴

-   检索和应用更新运营商设置 XML

-   向用户显示一条通知

如果你想要显示在应用中，通过触发后台任务的消息[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件必须读取消息内容并将消息内容存储在应用自己的本地数据存储中。 移动宽带短信平台不维护的队列接收管理短信通知。

### <a name="span-idmobilenetworkoperatorsmsnotificationsspanspan-idmobilenetworkoperatorsmsnotificationsspanspan-idmobilenetworkoperatorsmsnotificationsspanmobile-network-operator-sms-notifications"></a><span id="Mobile_network_operator_SMS_notifications"></span><span id="mobile_network_operator_sms_notifications"></span><span id="MOBILE_NETWORK_OPERATOR_SMS_NOTIFICATIONS"></span>移动网络运营商短信通知

传入的 SMS 消息可供任何应用，它具有请求并被授予访问权限的计算机上的 SMS 功能。 然而，某些 SMS 消息直接来自运营商，应将限制为和由移动宽带应用处理。

移动宽带短信平台筛选每个新收到的短信到两种类型之一： 管理 （无提示） 的短信通知从移动网络运算符 (MNO) 和常规短信。 管理 m n O 从收到的短信通知仅移动宽带应用可以访问，而隐藏的常规 SMS 客户端应用程序。

Mno 帐户预配的元数据中指定管理的 SMS 和 USSD 通知的自定义筛选的规则。 如果未不指定任何消息筛选规则，短信平台将所有短信都分类为可供任何应用程序的常规短信。 如果传入短信与预配的筛选规则，匹配[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)触发事件和后台工作项可以处理传入的 SMS 消息。

### <a name="span-idnetwork-initiatedussdspanspan-idnetwork-initiatedussdspanspan-idnetwork-initiatedussdspannetwork-initiated-ussd"></a><span id="Network-initiated_USSD"></span><span id="network-initiated_ussd"></span><span id="NETWORK-INITIATED_USSD"></span>网络启动 USSD

Windows 8、 Windows 8.1 和 Windows 10 提供了一个 USSD 的 API，这是隐藏大部分的详细信息，以简化应用程序开发的基础 USSD 协议的抽象。 在收到匹配预配的网络启动 USSD 后筛选规则， [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)触发事件和相应的后台工作项可以通过 USSD 会话使用通信USSD API。

有关 USSD Api 的详细信息，请参阅[ **Windows.Networking.NetworkOperators** ](https://msdn.microsoft.com/library/windows/apps/br241148)命名空间。

## <a name="span-idtriglocspanspan-idtriglocspantriggering-data-usage-and-roaming-notifications"></a><span id="trigloc"></span><span id="TRIGLOC"></span>触发数据使用情况和漫游通知


多个方面，Mno 需要法规法律用户达到其数据使用情况限制或更高的网络上漫游时通知用户。 此使用者保护应使用率过高的费用的风险。 在 Windows 中，移动宽带应用可以显示 toast 通知和磁贴更新，以让用户知道数据使用情况和漫游状态。 这些通知可以从启动网络后端通过使用 SMS 或 USSD，结果会触发[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件。 或者，可以通过在以下情况下使用本地信息触发 MobileOperatorNotification 事件。

### <a name="span-iddatausagenotificationbyusinglocaldatacountersspanspan-iddatausagenotificationbyusinglocaldatacountersspanspan-iddatausagenotificationbyusinglocaldatacountersspandata-usage-notification-by-using-local-data-counters"></a><span id="Data_usage_notification_by_using_local_data_counters"></span><span id="data_usage_notification_by_using_local_data_counters"></span><span id="DATA_USAGE_NOTIFICATION_BY_USING_LOCAL_DATA_COUNTERS"></span>使用本地数据计数器的数据使用情况通知

1.  使用预配的元数据启用本地数据使用情况通知。

2.  本地数据计数器估计自上次更新以来已更改的 5%以上的用户的数据限制的配置文件的使用情况。

3.  数据使用情况和订阅管理器 (DUSM) 通知系统事件代理，以触发[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件。

4.  系统事件代理调用的移动宽带应用来处理后台事件。

5.  应用程序通过检索最新的使用情况信息从后端基础结构处理事件。

6.  如果当前使用情况信息超出了阈值 （如 80%)，该应用程序向用户显示一条 toast 通知，并使用当前使用情况更新 DUSM。 或者，如果当前使用情况不超过阈值，应用程序不必显示 toast 通知。

### <a name="span-idroamingnotificationbyusingwindowsconnectionmanagerspanspan-idroamingnotificationbyusingwindowsconnectionmanagerspanspan-idroamingnotificationbyusingwindowsconnectionmanagerspanroaming-notification-by-using-windows-connection-manager"></a><span id="Roaming_notification_by_using_Windows_Connection_Manager"></span><span id="roaming_notification_by_using_windows_connection_manager"></span><span id="ROAMING_NOTIFICATION_BY_USING_WINDOWS_CONNECTION_MANAGER"></span>使用 Windows 连接管理器的漫游通知

1.  漫游的移动宽带网络上注册 Windows 连接管理器。

2.  Windows 连接管理器会通知系统事件代理，以触发[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件。

3.  系统事件代理调用移动运营商应用程序以处理后台事件。

4.  应用程序标识是否在此网络上漫游时，用户会产生额外的使用量费用和有必要，向用户显示 toast 通知和磁贴更新。

## <a name="span-idexpirespanspan-idexpirespandata-plan-expiration-and-usage-reset"></a><span id="expire"></span><span id="EXPIRE"></span>数据计划过期时间和使用情况重置


DUSM 跟踪用户的帐户或帐户，包括预付费的数据计划的计划到期日期的详细信息或计划使用情况重置后付费的数据计划的日期。 当用户的数据计划过期时，DUSM 通知系统事件代理，以触发[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件。 移动宽带应用可以处理的事件，通过显示一条 toast 通知和磁贴更新通知他们其计划已过期或引导他们以续订其服务的用户。

如果后付费的数据计划，DUSM 将重置为零，在特定日期，例如每月的第一天的计划数据使用情况。 此操作时， [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)触发事件和应用程序可以通知用户其更新后的数据使用情况。

## <a name="span-idsharingspanspan-idsharingspanentitlement-check-for-internet-sharing"></a><span id="sharing"></span><span id="SHARING"></span>权利检查 Internet 共享


在 Windows 8.1 Internet 共享，通常称为 tethering，添加了以使用户能够与要为非移动的一个或多个其他设备共享他们的移动宽带网络连接宽带支持。 传统 tethering 机制包括 Bluetooth 和 USB。 但是，Wi-fi 可以提供快速并轻松共享机制，例如个人热点，移动热点，等，因为它需要一些配置的移动宽带连接实现高速数据传输，依赖于熟悉的 Wi-fi连接过程。

某些 Mno 或 Mvno 不支持 Internet 共享功能上的其网络或它们需要在设置共享 Internet 连接之前权利检查。 Windows 提供了必要的控件，以确保 Windows 设备符合网络策略。 如果移动运营商已设置[AllowTethering](allowtethering.md)元素**EntitlementCheckRequired**在服务元数据包，系统会触发[MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)事件。 移动宽带应用程序然后与网络服务，以检查用户可以使用 Internet 共享功能和响应系统通信。 如果允许用户使用该功能，Internet 共享将成功启动，否则用户将会显示默认错误消息或移动运营商定义的消息。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)

[创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)

 

 






