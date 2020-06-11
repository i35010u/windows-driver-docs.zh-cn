---
title: 了解和配置 Windows 连接管理器
description: 了解和配置 Windows 连接管理器
ms.assetid: 5ef0034f-5b30-4484-a11c-ed19931484a2
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0046844b912bdaebb3766d188bbf3383a7adf4fa
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681679"
---
# <a name="understanding-and-configuring-windows-connection-manager"></a>了解和配置 Windows 连接管理器

> [!IMPORTANT]
> 本主题适用于可配置 Windows 如何连接到其网络的 Microsoft 移动运营商（MO）合作伙伴。 如果你是遇到 Windows 网络连接问题的客户，请参阅[修复 windows 中的网络连接问题](https://support.microsoft.com/help/10741/windows-fix-network-connection-issues)。

Windows 8 中引入的自动连接管理通过查看以太网、Wi-fi 和移动宽带接口做出连接决策。 这些决策将导致 Wi-fi 和移动宽带接口上的自动连接和断开操作。

> [!NOTE]
> Windows 响应以太网连接，但不自动管理以太网连接。

本主题介绍 Windows 如何自动管理物理无线连接，并且不会考虑这些连接：

-   拨号连接，如调制解调器

-   纯虚拟接口，如 Vpn 和隧道 IP 连接

## <a name="span-idconnection_management_policiesspanspan-idconnection_management_policiesspanspan-idconnection_management_policiesspanconnection-management-policies"></a><span id="Connection_management_policies"></span><span id="connection_management_policies"></span><span id="CONNECTION_MANAGEMENT_POLICIES"></span>连接管理策略

Windows 8、Windows 8.1 和 Windows 10 提供了许多用于控制连接管理的策略。 这些策略不会在 Windows 用户界面中公开，但可以使用[WcmSetProperty](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetproperty) API 或组策略进行配置。

### <a name="span-idminimize_simultaneous_connectionsspanspan-idminimize_simultaneous_connectionsspanspan-idminimize_simultaneous_connectionsspanminimize-simultaneous-connections"></a><span id="Minimize_simultaneous_connections"></span><span id="minimize_simultaneous_connections"></span><span id="MINIMIZE_SIMULTANEOUS_CONNECTIONS"></span>同时最小化连接

此策略使用**fMinimizeConnections**组策略进行配置。 默认情况下，它在 Windows 8、Windows 8.1 和 Windows 10 上处于启用状态。

#### <a name="versions-of-windows-before-windows-10-version-1809-build-17763404"></a>Windows 10 之前的 Windows 版本1809，版本17763.404

在 windows 8、Windows 8.1 和 windows 10 版本1809之前的 windows 10 版本17763.404 中，此策略是一个可以使用组策略或[WcmSetProperty](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetproperty) API 修改的布尔值。

如果禁用此策略，则行为类似于 Windows 7 的行为，在这种情况下，每个接口会连接到最优先的网络（在范围内），而不考虑其他接口的连接状态。

如果启用此策略，则 Windows 将尝试保持最小数量的并发连接，以提供最佳的可用连接级别。 Windows 保持连接到以下网络：

-   任何以太网网络

-   当前用户会话期间手动连接的任何网络

-   与 Internet 的首选连接

-   如果 PC 加入到域，则连接到 Active Directory 域的最首选连接

所有剩余网络均已软断开连接，如下一节中所述。 这也可用于评估未连接的可用网络。 Windows 不会连接到新网络，这样它就可以立即进行软断开连接。

#### <a name="windows-10-version-1809-build-17763404-and-later"></a>Windows 10，版本1809，版本17763.404 及更高版本

在 Windows 10 版本1809、版本17763.404 和更高版本中，此值是只能通过组策略提供的枚举。

此策略设置确定一台计算机能否有多个连接到 Internet、Windows 域或两个连接。 如果允许多个连接，则策略将确定如何路由网络流量。

如果将此策略设置为**0**，则计算机可以同时连接到 Internet、Windows 域或两者。 Internet 流量可以通过任何连接进行路由，包括蜂窝连接或任何按流量计费的网络。 在 Windows 10 版本1809之前的 Windows 版本中17663.404，此策略设置以前是此策略设置的*禁用*状态。 此选项在 Windows 8 中首次可用。

如果此策略设置为**1**，则在计算机至少有一个与首选网络类型的活动 Internet 连接时，将阻止任何新的自动 Internet 连接。 优先顺序如下：

1. 以太网
2. WLAN
3. 移动电话

连接时，以太网始终是首选的。 用户仍可手动连接到任何网络。 在 Windows 10 版本1809之前的 Windows 版本中17763.404，此策略设置以前是此策略设置的 "*已启用*" 状态。 此选项在 Windows 8 中首次可用。

如果此策略设置设置为**2**，则该行为在设置为**1**时类似于。 但是，如果手机网络数据连接可用，则该连接将始终保持连接，以获取需要蜂窝连接的服务。 当用户连接到 WLAN 或以太网连接时，不会通过移动电话连接来路由 Internet 流量。 此选项最初在 Windows 10 版本1703中提供。

如果此策略设置设置为**3**，则该行为在设置为**2**时类似于。 但是，如果有以太网连接，Windows 将不允许用户手动连接到 WLAN。 如果没有以太网连接，WLAN 只能连接（自动或手动）。

### <a name="span-idsoft_disconnectspanspan-idsoft_disconnectspanspan-idsoft_disconnectspansoft-disconnect"></a><span id="Soft_disconnect"></span><span id="soft_disconnect"></span><span id="SOFT_DISCONNECT"></span>软断开

软断开连接策略的工作方式如下：

1.  当 Windows 决定不再连接某个网络时，它不会立即断开连接。 突然断开会降低用户体验，而无需提供明显权益，并尽可能避免使用。

2.  一旦 Windows 决定软断开连接接口，就会通知 TCP 堆栈网络不应再使用。 现有的 TCP 会话将继续不间断，但新的 TCP 会话仅当显式绑定或没有其他任何接口路由到所需目标时才使用此接口。

3.  此通知到 TCP 堆栈会生成网络状态更改。 网络应用程序应该侦听这些事件，并在可能的情况下主动将其连接转移到新的网络。

4.  然后，Windows 每隔30秒检查一次接口的流量级别。 如果流量级别超过特定阈值，则不执行其他操作。 这允许当前有效使用接口，如文件传输或 VoIP 调用，以避免中断。

5.  当流量低于此阈值时，接口将断开连接。 保持长期空闲连接的应用程序（例如电子邮件客户端）可能会被中断，并应通过不同的接口重新建立连接。

### <a name="span-idinitial_connectionspanspan-idinitial_connectionspanspan-idinitial_connectionspaninitial-connection"></a><span id="Initial_connection"></span><span id="initial_connection"></span><span id="INITIAL_CONNECTION"></span>初始连接

在一种情况下，Windows 会自动连接，然后立即软断开。 当电脑首次启动或从待机状态恢复时，所有接口同时尝试连接，以确保用户尽快获得网络连接。 如果多个接口成功连接，则 Windows 将立即开始软断开连接接口。

### <a name="span-idprohibit_interconnect_between_domain_and_non-domain_networksspanspan-idprohibit_interconnect_between_domain_and_non-domain_networksspanspan-idprohibit_interconnect_between_domain_and_non-domain_networksspanprohibit-interconnect-between-domain-and-non-domain-networks"></a><span id="Prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="PROHIBIT_INTERCONNECT_BETWEEN_DOMAIN_AND_NON-DOMAIN_NETWORKS"></span>禁止域和非域网络之间的互连

默认情况下，此策略在 Windows 8、Windows 8.1 和 Windows 10 中处于关闭状态。 如果启用此策略，则 Windows 将尝试防止计算机在域网络和非域网络之间建立连接。 当使用多宿主计算机作为攻击点时，企业管理员可能会使用此项。

当所有连接的网络路由到域或没有连接的网络路由到域时，此策略不会影响系统行为。

### <a name="span-idmultiple_wireless_networksspanspan-idmultiple_wireless_networksspanspan-idmultiple_wireless_networksspanmultiple-wireless-networks"></a><span id="Multiple_wireless_networks"></span><span id="multiple_wireless_networks"></span><span id="MULTIPLE_WIRELESS_NETWORKS"></span>多个无线网络

许多 Windows 8、Windows 8.1 和 Windows 10 移动版设备在任何时候都有可供他们使用的外部 Internet 连接，即使是在其企业的 Wi-fi 网络范围内。 启用此策略后，用户可以自由连接到其公共移动宽带网络或企业的专用 Wi-fi 网络，并在它们之间进行切换。 但是，手动连接一个将自动导致另一个连接立即断开。

### <a name="span-idethernetspanspan-idethernetspanspan-idethernetspanethernet"></a><span id="Ethernet"></span><span id="ethernet"></span><span id="ETHERNET"></span>网

由于 Windows 8、Windows 8.1 和 Windows 10 无法自动将以太网电缆连接到或断开连接，因此它们只能通过允许或禁止无线连接来强制执行该策略。 当电脑与域网络建立以太网连接时，不能连接到域的无线网络无法连接，反之亦然。 如果尝试这样做，将导致以下错误：

![自动连接管理错误](images/mb-acm-1.png)

对于具有多个以太网端口的 Pc，Windows 无法阻止通过物理方式将电脑连接到两个不同的以太网网络而创建的互连。

### <a name="span-ideffect_on_soft_disconnectspanspan-ideffect_on_soft_disconnectspanspan-ideffect_on_soft_disconnectspaneffect-on-soft-disconnect"></a><span id="Effect_on_soft_disconnect"></span><span id="effect_on_soft_disconnect"></span><span id="EFFECT_ON_SOFT_DISCONNECT"></span>软断开连接效果

由于禁止互连是一种安全考虑因素，符合此策略的任何断开都将立即生效，即使正在进行活动也是如此。 即使两个网络重叠，用户在公共网络与企业网络之间过渡时也会遇到连接中断。

例如，通过移动宽带网络（插接到公司以太网连接的便携式计算机）进行的 VoIP 调用的用户将失去呼叫，但应用可能能够通过新连接自动恢复。 如果未启用该策略，则 Windows 将通过等待调用完成来软断开移动宽带连接。 另一方面，在连接到公司网络时，通过公司 Wi-fi 网络启动的 VoIP 呼叫不会中断，因为这两个网络都连接到域。 调用完成后，Wi-fi 网络将断开连接。

### <a name="span-idprohibit_roaming_on_mobile_broadband_networksspanspan-idprohibit_roaming_on_mobile_broadband_networksspanspan-idprohibit_roaming_on_mobile_broadband_networksspanprohibit-roaming-on-mobile-broadband-networks"></a><span id="Prohibit_roaming_on_mobile_broadband_networks"></span><span id="prohibit_roaming_on_mobile_broadband_networks"></span><span id="PROHIBIT_ROAMING_ON_MOBILE_BROADBAND_NETWORKS"></span>禁止在移动宽带网络上漫游

此策略阻止 Windows 连接到处于漫游状态的移动宽带网络。 默认情况下，禁用此策略，用户可以选择在漫游时手动连接到移动宽带网络，或启用自动连接到此类网络。 如果启用此策略，用户将无法从连接管理器中选择漫游移动宽带网络。

## <a name="span-idnetwork_preferencesspanspan-idnetwork_preferencesspanspan-idnetwork_preferencesspannetwork-preferences"></a><span id="Network_preferences"></span><span id="network_preferences"></span><span id="NETWORK_PREFERENCES"></span>网络首选项


考虑维护哪多个连接时，Windows 将使用多种特征来确定首选网络。 仅当确定是否维持到给定接口（而不是路由）的连接时，才使用此。 如果连接的接口不处于软断开连接的过程中，则路由由路由表中的度量值决定。 如果未手动指定路由指标，Windows 将根据适配器的链接速度自动分配路由指标。

### <a name="span-idconnection_prioritiesspanspan-idconnection_prioritiesspanspan-idconnection_prioritiesspanconnection-priorities"></a><span id="Connection_priorities"></span><span id="connection_priorities"></span><span id="CONNECTION_PRIORITIES"></span>连接优先级

Windows 按下列顺序为连接排定优先级：

1.  以太网网络

2.  当前用户会话期间手动连接的网络

3.  同时连接到 Internet 的网络和 PC 加入到的 Active Directory 域

4.  当前连接的 Wi-fi 网络的信号强度

5.  计算机的首选网络列表

即使链接速度影响当前连接的接口之间的路由行为，Windows 也不会根据网络的链接速度或吞吐量做出连接决定。 不能将 Windows 配置为基于移动宽带网络的当前速度更改移动宽带网络与 Wi-fi 网络之间的连接首选项。 如果两者都处于连接状态，则用户或桌面应用程序可以更改路由指标以影响路由首选项。

### <a name="span-idsignal_strengthspanspan-idsignal_strengthspanspan-idsignal_strengthspansignal-strength"></a><span id="Signal_strength"></span><span id="signal_strength"></span><span id="SIGNAL_STRENGTH"></span>信号强度

对于 Windows 8 和 Windows 8.1，如果 Windows 检测到当前连接的 Wi-fi 网络的信号强度非常低，则可以选择连接移动宽带网络（如果策略允许）以避免中断网络连接。 这有助于在用户离开无线接入点时平滑转换。

Windows 不会断开更喜欢的 Wi-fi 网络，直到信号强度无法维持连接。 如果信号强度提高，Windows 可能会对移动宽带适配器进行软断开连接。

Windows 10 不使用 Wi-fi 信号强度。

### <a name="span-idpreferred_network_listspanspan-idpreferred_network_listspanspan-idpreferred_network_listspanpreferred-network-list"></a><span id="Preferred_network_list"></span><span id="preferred_network_list"></span><span id="PREFERRED_NETWORK_LIST"></span>首选网络列表

在大多数情况下，首选网络列表将确定 Windows 要用于连接的无线网络配置文件。 在 Windows 8 之前，此列表仅适用于 Wi-fi 网络。 在 Windows 8、Windows 8.1 和 Windows 10 中，它还可以包括移动宽带网络。

### <a name="span-idautomatic_generationspanspan-idautomatic_generationspanspan-idautomatic_generationspanautomatic-generation"></a><span id="Automatic_generation"></span><span id="automatic_generation"></span><span id="AUTOMATIC_GENERATION"></span>自动生成

Windows 8、Windows 8.1 和 Windows 10 会根据用户操作自动更新首选网络列表。 任何手动连接或断开连接都将更新网络列表，以便在将来自动发生相同的行为。

以下用户操作修改首选网络列表：

-   **最初连接到网络**新的网络将添加到网络列表中。 用户指定将来是否会自动连接网络。

    -   第一次连接到新的 Wi-fi 网络后，网络就会成为列表中最优先的网络。

    -   首次连接到新的移动宽带网络，使网络成为列表中首选的最小网络。

-   **手动连接到 wi-fi 网络**列表中较高范围内的任何其他 Wi-fi 网络将移动到列表中新连接的网络下。 用户指定网络将来是否自动连接。

-   **断开与网络的连接**Windows 将来不会自动连接到该网络。 它保留在网络列表中，以防用户在将来修改此设置。

### <a name="span-idgroup_policyspanspan-idgroup_policyspanspan-idgroup_policyspangroup-policy"></a><span id="Group_Policy"></span><span id="group_policy"></span><span id="GROUP_POLICY"></span>组策略

组策略创建的 wi-fi 配置文件位于网络列表的顶部。 用户可以手动从这些网络断开连接，也可以手动连接到其他网络，但在组策略删除之前，这些网络将在网络列表中一直保持最高位置。

### <a name="span-idcarrier-provisioning_metadataspanspan-idcarrier-provisioning_metadataspanspan-idcarrier-provisioning_metadataspancarrier-provisioning-metadata"></a><span id="Carrier-provisioning_metadata"></span><span id="carrier-provisioning_metadata"></span><span id="CARRIER-PROVISIONING_METADATA"></span>运营商-设置元数据

移动宽带和 Wi-fi 热点操作员使用[**ProvisioningAgent**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)或[**MsProvisionNetworks**](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85)) api 为 Windows 提供一系列移动宽带和 wi-fi 配置文件。

初始预配时，操作员创建的配置文件将添加到现有网络列表的顶部（仅适用于 Wi-fi）或底部（如果包含移动宽带）。 不能影响用户在网络列表中设置的网络位置。 但是，你可以在网络列表中定义其网络的相对顺序。

用户的操作可能会在预配元数据的应用程序之间修改网络列表。 重新应用预配元数据时，所需的网络顺序将被还原。 但是，重新排序的网络集会移到用户已将任何网络移动到的最小位置。

设置元数据中网络之间的首选项由以下各项决定：

1.  每个网络配置文件的可选优先级属性

2.  媒体类型（Wi-fi 比移动宽带更首选）

3.  XML 文件中指定的顺序

### <a name="span-idmanual_modificationspanspan-idmanual_modificationspanspan-idmanual_modificationspanmanual-modification"></a><span id="Manual_modification"></span><span id="manual_modification"></span><span id="MANUAL_MODIFICATION"></span>手动修改

在 Windows 8 之前，用户可以通过 "管理无线网络" 控制面板访问 Wi-fi 首选网络列表。 遥测表明很少有用户曾访问过此功能。 此外，此用户界面仅限于 Wi-fi，无法在 Wi-fi 和移动宽带之间引入首选项。

大多数用户不需要手动修改网络列表。 但是，某些用户或应用程序可能会发现有必要这样做。

### <a name="span-iduser_interfacespanspan-iduser_interfacespanspan-iduser_interfacespanuser-interface"></a><span id="User_interface"></span><span id="user_interface"></span><span id="USER_INTERFACE"></span>用户界面

若要在配置文件处于范围内时从首选网络列表中删除配置文件，请右键单击该网络，然后选择 "**忘记此网络**"。 不在范围内的网络不能通过用户界面从列表中删除。

### <a name="span-idwin32_apisspanspan-idwin32_apisspanspan-idwin32_apisspanwin32-apis"></a><span id="Win32_APIs"></span><span id="win32_apis"></span><span id="WIN32_APIS"></span>Win32 Api

应用程序可以使用适当的媒体特定 API 在网络列表中创建新的配置文件：

-   对于 Wi-fi 网络，使用[**WlanSetProfile**](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlansetprofile)函数。

-   对于移动宽带网络，请使用[**IMbnConnectionProfileManager：： CreateConnectionProfile**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionprofilemanager-createconnectionprofile)方法。

若要修改网络列表的顺序，请使用[**WcmSetProfileList**](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetprofilelist)函数。 不建议使用[**WlanSetProfileList**](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlansetprofilelist)函数，因为它可能会以意外的方式干扰网络列表中移动宽带配置文件的位置。

若要从网络列表中删除配置文件，请使用相应的媒体特定 API：

-   对于 Wi-fi 网络，使用[**WlanDeleteProfile**](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlandeleteprofile)函数。

-   对于移动宽带网络，请使用[**IMbnConnectionProfile：:D e)**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionprofile-delete)方法。

### <a name="span-idcommand-linespanspan-idcommand-linespanspan-idcommand-linespancommand-line"></a><span id="Command-line"></span><span id="command-line"></span><span id="COMMAND-LINE"></span>命令行

用户或脚本可以通过使用相应的媒体特定命令，在网络列表中创建新的配置文件：

-   对于 Wi-fi 网络，请使用**netsh wlan add profile**命令。

-   对于移动宽带网络，请使用**netsh mbn add profile**命令。

可以使用**netsh wlan set profileorder**命令修改网络列表中的 wi-fi 配置文件的顺序。 但是，不建议这样做，并且可能会以意外的方式扰乱列表中移动宽带配置文件的位置。

若要从网络列表中删除配置文件，请使用相应的媒体特定命令：

-   对于 Wi-fi 网络，请使用**netsh wlan delete profile**命令。

-   对于移动宽带网络，请使用**netsh mbn delete profile**命令。

### <a name="span-idconflict_resolutionspanspan-idconflict_resolutionspanspan-idconflict_resolutionspanconflict-resolution"></a><span id="Conflict_resolution"></span><span id="conflict_resolution"></span><span id="CONFLICT_RESOLUTION"></span>冲突解决

当同一网络存在多个配置文件时，Windows 8 和 Windows 8.1 使用以下逻辑来确定应使用的配置文件：

1.  **“配置文件类型”**

    1.  组策略配置文件优于用户创建的配置文件。

    2.  所有用户配置文件优于单一用户配置文件。

2.  **接口到达**将使用最近安装的接口上的配置文件。

 

 





