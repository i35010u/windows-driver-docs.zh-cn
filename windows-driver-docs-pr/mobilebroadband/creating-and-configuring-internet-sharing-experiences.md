---
title: 创建和配置 Internet 共享体验
description: 创建和配置 Internet 共享体验
ms.assetid: 11906ee4-68f5-4be6-a3ab-6af3253c8a11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5e23f4369bac1140339ab487dbd18b21f57280a
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304282"
---
# <a name="creating-and-configuring-internet-sharing-experiences"></a>创建和配置 Internet 共享体验


Internet 共享（通常称为 tethering）已添加到 Windows 8.1 中，可让用户与一个或多个不支持移动宽带的设备共享其移动宽带网络连接。 传统的 tethering 机制包括蓝牙和 USB。 但是，Wi-fi 可以提供快速轻松的移动宽带连接共享机制（如个人热点、移动热点等），因为它只需很少的配置，可实现高速数据传输，并依赖于熟悉的 Wi-fi 连接过程。

Windows 8.1 和 Windows 10 通过使客户能够启用和连接到已配置 Internet 共享的电脑（称为 tethering 接入点，就像是标准 Wi-fi 网络），进一步扩展 Internet 共享功能。

## <a name="span-idturn_on_internet_sharingspanspan-idturn_on_internet_sharingspanspan-idturn_on_internet_sharingspanturn-on-internet-sharing"></a><span id="Turn_on_Internet_Sharing"></span><span id="turn_on_internet_sharing"></span><span id="TURN_ON_INTERNET_SHARING"></span>启用 Internet 共享


可以使用支持移动宽带的设备上的 "设置" 超级按钮打开 Internet 共享。 启用 Internet 共享后，任何能够连接到 Wi-fi 网络的设备都可以连接到该网络。

**启用 Internet 共享**

1.  在 " **设置** " 超级按钮中，单击 " **更改电脑设置**"，然后单击 " **网络**"。

2.  在 **移动宽带** 标题下，单击网络名称。

3.  在 **移动宽带** 页面上，为网络启用 Internet 共享。 如果移动宽带网络断开连接，则在设置 Wi-fi 网络之前，设备将自动连接到移动宽带网络。

4.  如果已创建了必需的服务元数据包，则 PC 会触发一个事件，告诉 Microsoft Store 移动宽带应用运行权利检查。 电脑在启用 Internet 共享之前，会等待移动宽带应用响应。 有关创建服务元数据包的详细信息，请参阅 [创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

5.  启用移动宽带网络并已通过任何所需的权利检查后，将通过使用将 Wi-fi Direct 自治组所有者模式与自定义网络名称一起使用的专用 Wi-fi 网络来共享移动宽带连接。 这可确保任何 Wi-fi 设备都可以连接到网络。

    **注意**   移动宽带网络的图标在整个 Windows 中自动更新，以帮助客户记住，网络正被其他人共享。

     

6.  打开 Internet 共享后，在 " **移动宽带** " 页上，单击 " **编辑** " 以更改网络名称和密码。

    -   Wi-fi 网络必须使用 WPA2-PSK。

    -   网络名称设置为默认的* &lt; 设备名称 &gt; &lt; 4 位数字 &gt; *。 默认网络名称经过优化，以确保用户可以识别该名称，因为该名称足够短，足以完全容纳在网络列表中，并且足以区分多个设备。

    -   密码设置为默认值12个随机数字。

    -   密码长度必须至少为8个字符。

    -   当网络名称或密码更改时，Wi-fi 网络将重新启动。

打开 Internet 共享时，会发生以下情况：

-   客户端设备上的网络自动设置为按流量计费的连接，以减少移动宽带网络上不必要的带宽消耗。 这是通过在定义网络开销的 Wi-fi 信标/探测响应帧中使用特定于 Windows 8 供应商的信息元素来完成的。 在 Windows 8.1 添加了 Wi-fi 信标/探测响应帧中其他特定于供应商的信息元素，该元素会在网络为 tethering 网络时通知客户端设备。 此添加会影响 Windows 8.1 和 Windows 10。

-   打开 Internet 共享时，PC 无法进入连接待机或睡眠状态，以确保客户端设备不会失去其 Internet 连接。

-   你可以通过使用移动宽带应用来查看客户端设备已使用的数据量。

-   最后一台客户端设备从受限网络断开连接后，Internet 共享将等待5分钟。 如果未连接任何其他客户端设备，则会关闭 Internet 共享，并且 PC 会恢复正常电源状态。

-   企业管理员可以使用组策略禁用 Internet 共享。

## <a name="span-idconnect_to_a_tethered_networkspanspan-idconnect_to_a_tethered_networkspanspan-idconnect_to_a_tethered_networkspanconnect-to-a-tethered-network"></a><span id="Connect_to_a_tethered_network"></span><span id="connect_to_a_tethered_network"></span><span id="CONNECT_TO_A_TETHERED_NETWORK"></span>连接到受限网络


你可以使用 Wi-fi 设备连接到受限网络，就像连接到任何其他 Wi-fi 网络一样。 但是，如果用户使用 Windows 8.1 或 Windows 10 上运行的两台设备上的相同 Microsoft 帐户凭据连接到受限网络，则会发生以下情况：

-   如果在 Windows 8.1 或 Windows 10 设备连接时未打开 Internet 共享，则这两个设备将创建一个蓝牙连接，并且打开 Internet 共享。

-   通过自动从受限网络检索凭据 (网络名称和 SSID) 自动配置连接。

**注意**   如果用户已通过使用 Bluetooth 配对其设备，还可以连接到 tethering 接入点。

 

## <a name="span-idconfigure_internet_sharingspanspan-idconfigure_internet_sharingspanspan-idconfigure_internet_sharingspanconfigure-internet-sharing"></a><span id="Configure_Internet_Sharing"></span><span id="configure_internet_sharing"></span><span id="CONFIGURE_INTERNET_SHARING"></span>配置 Internet 共享


某些移动网络操作员 (Mno) 或移动虚拟网络运营商 (Mvno) 在其网络上不支持 Internet 共享，或者在设置 Internet 共享之前需要进行权利检查。 Windows 提供必要的控件，以确保 Windows 设备符合网络策略。 

若要在 Windows 8、Windows 8.1 或 Windows 10 版本1803之前执行此操作，必须编写服务元数据包，并在架构 ([服务元数据包架构参考](mobilebroadbandinfo-xml-schema.md)) 中配置[AllowTethering](allowtethering.md)元素。 有关创建服务元数据包的详细信息，请参阅 [创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。 有三个选项：

-   允许所有客户进行 Internet 共享。 如果服务元数据包中未指定 (默认值) 

-   阻止所有客户的 Internet 共享

-   授权检查后允许客户进行 Internet 共享

若要在 Windows 10 版本1803及更高版本中执行此操作，必须将[COSA 数据库中的**热点**设置](desktop-cosa-apn-database-settings.md#desktop-cosa-only-settings)设置为合适的值。

如果你决定不需要权限检查，则不需要其他信息或功能。 如果需要权限检查，还必须提供作为 UWP mobile 宽带应用的一部分的背景通知事件处理程序。 在 Windows 10 版本1803及更高版本中，使用 [TetheringEntitlementCheckTriggerDetails](/uwp/api/windows.networking.networkoperators.tetheringentitlementchecktriggerdetails) 类中的方法来处理 Windows 通知事件，以便检查 tethering 权限。 对于早期版本的 Windows，请使用 [**NetworkOperatorNotificationEventDetails**](/uwp/api/Windows.Networking.NetworkOperators.NetworkOperatorNotificationEventDetails) 类。 有关创建后台通知事件处理程序的详细信息，请参阅 [启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

MOs 和 Mvno 对用于 Internet 共享的 PDP 上下文有不同的要求。 Windows 已更新现有的 [预配 XML 架构](/uwp/schemas/mobilebroadbandschema/schema-for-mobile-broadband-portal) ，使你能够使用正确的 INTERNET 共享 PDP 上下文信息来预配系统。 有关多个 PDP 上下文的详细信息，请参阅 [使用多个 pdp 上下文开发应用](developing-apps-using-multiple-pdp-contexts.md)。

你还可以配置10个并发连接的客户端设备的最大数量。 可以使用 [帐户预配](account-provisioning.md)将此数字更改为3到10之间的任何值。

若要帮助确保用户不会意外地对其数据运行，可以通过使用[**ConnectionProfile**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile)类的[**GetNetworkUsageAsync**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkUsageAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_DataUsageGranularity_Windows_Networking_Connectivity_NetworkUsageStates_)方法，向客户显示移动宽带应用中共享和非共享流量的数据使用情况统计信息。

## <a name="span-idcreate_a_custom_internet_sharing_appspanspan-idcreate_a_custom_internet_sharing_appspanspan-idcreate_a_custom_internet_sharing_appspancreate-a-custom-internet-sharing-app"></a><span id="Create_a_custom_Internet_Sharing_app"></span><span id="create_a_custom_internet_sharing_app"></span><span id="CREATE_A_CUSTOM_INTERNET_SHARING_APP"></span>创建自定义 Internet 共享应用


对于大多数操作员，Windows 用户界面将为 Internet 共享提供最佳体验。 但是，若要在其所有设备和硬件中创建一致的体验，你可以选择在移动宽带应用或其他应用中包括你自己的 Internet 共享用户体验，这些用户已被授予移动宽带设备的特权访问权限。 Windows 在 [**windows.networking.networkoperators 命名空间**](/uwp/api/Windows.Networking.NetworkOperators) 中提供了几个新的 api，使您的应用程序可以执行以下操作：

-   确保系统能够进行 Internet 共享

-   打开和关闭 Internet 共享

-   查询并配置适用于网络的 Wi-fi SSID 和密码

-   运行权利检查

-   查询连接的设备数，以及允许的最大连接设备数

-   接收和响应有关 Internet 共享状态或连接设备数的更改的通知

 

