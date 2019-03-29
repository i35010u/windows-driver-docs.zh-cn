---
title: 了解和配置 Windows 连接管理器
description: 了解和配置 Windows 连接管理器
ms.assetid: 5ef0034f-5b30-4484-a11c-ed19931484a2
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7203fb01847ce67f6913b25b7209b3fb70a6c0ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566259"
---
# <a name="understanding-and-configuring-windows-connection-manager"></a>了解和配置 Windows 连接管理器

> [!IMPORTANT]
> 本主题适用于 Microsoft 的移动运营商 （月） 的合作伙伴可以配置 Windows 连接到其网络的方式。 如果您遇到 Windows 网络连接问题的客户，请参阅[在 Windows 中修复网络连接问题](https://support.microsoft.com/help/10741/windows-fix-network-connection-issues)。

自动连接管理，Windows 8 中引入做出连接决策通过查看以太网、 Wi-fi 和移动宽带接口。 这些决策潜在客户为自动连接和断开连接的 Wi-fi 和移动宽带接口上的操作。

**请注意**   Windows 响应以太网连接，但不会自动管理以太网连接。

 

本主题介绍 Windows 自动如何管理物理无线连接，而不考虑这些连接：

-   拨号连接，例如调制解调器

-   纯虚拟接口，例如 Vpn 或隧道的 IP 连接

## <a name="span-idconnectionmanagementpoliciesspanspan-idconnectionmanagementpoliciesspanspan-idconnectionmanagementpoliciesspanconnection-management-policies"></a><span id="Connection_management_policies"></span><span id="connection_management_policies"></span><span id="CONNECTION_MANAGEMENT_POLICIES"></span>连接管理策略


Windows 8、 Windows 8.1 和 Windows 10 包括许多控制连接管理的策略。 这些策略在 Windows 用户界面中不公开但可以通过使用配置[WcmSetProperty](https://msdn.microsoft.com/library/windows/desktop/hh437602.aspx) API 或组策略。

### <a name="span-idminimizesimultaneousconnectionsspanspan-idminimizesimultaneousconnectionsspanspan-idminimizesimultaneousconnectionsspanminimize-simultaneous-connections"></a><span id="Minimize_simultaneous_connections"></span><span id="minimize_simultaneous_connections"></span><span id="MINIMIZE_SIMULTANEOUS_CONNECTIONS"></span>最大程度减少同时连接

使用配置此策略**fMinimizeConnections**组策略。 它是默认情况下，适用于 Windows 8、 Windows 8.1 和 Windows 10 上。 如果禁用此策略，则行为将类似于 Windows 7 中的每个接口连接到最适合的网络在范围内，而不考虑其他接口的连接状态。

如果启用此策略，Windows 将尝试维护的最小提供最佳的可用连接级别的并发连接数。 Windows 维护以下网络的连接：

-   任何以太网网络

-   当前用户会话期间手动连接任何网络

-   优先级最高的连接到 Internet

-   与 Active Directory 域，如果电脑已加入域的优先级最高的连接

剩余的所有网络软件的断开都连接下, 一节中所述。 这用于评估可用的网络未连接的。 Windows 将连接到从中它会立即软-断开连接的新网络。

### <a name="span-idsoftdisconnectspanspan-idsoftdisconnectspanspan-idsoftdisconnectspansoft-disconnect"></a><span id="Soft_disconnect"></span><span id="soft_disconnect"></span><span id="SOFT_DISCONNECT"></span>软断开连接

软断开连接的方式是以下：

1.  当 Windows 决定应不再连接网络时，它不会立即断开。 突然断开连接而无需提供明显的好处，降低用户体验，并避免了在可能的情况。

2.  只要 Windows 决定软断开一个接口，它通知 TCP 堆栈，应不再使用网络。 现有的 TCP 会话将不间断地继续，但新 TCP 会话将使用此接口仅当显式绑定的或如果没有其他界面将路由到所需的目标。

3.  对 TCP 堆栈此通知会生成网络状态更改。 网络应用程序应侦听这些事件并主动移动其连接到新网络时，在可能的情况。

4.  Windows 然后检查该接口上的流量级别每隔 30 秒。 如果流量级别超过特定阈值，则不采取任何进一步的操作。 这允许正在进行的活动使用的接口，例如从文件传输或 VoIP 呼叫，以避免中断。

5.  当流量低于此阈值时，该接口将断开连接。 应用程序保留生存期较长的空闲连接，如电子邮件客户端，可能会中断，并且通过不同接口重新建立连接。

### <a name="span-idinitialconnectionspanspan-idinitialconnectionspanspan-idinitialconnectionspaninitial-connection"></a><span id="Initial_connection"></span><span id="initial_connection"></span><span id="INITIAL_CONNECTION"></span>初始连接

Windows 会自动连接，然后立即软-断开连接在一种情况下。 当 PC 首次启动或从待机状态恢复时，所有接口同时都尝试连接，以便确保用户尽可能快地获取网络连接。 如果已成功连接多个接口，Windows 会立即开始软断开连接的接口。

### <a name="span-idprohibitinterconnectbetweendomainandnon-domainnetworksspanspan-idprohibitinterconnectbetweendomainandnon-domainnetworksspanspan-idprohibitinterconnectbetweendomainandnon-domainnetworksspanprohibit-interconnect-between-domain-and-non-domain-networks"></a><span id="Prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="PROHIBIT_INTERCONNECT_BETWEEN_DOMAIN_AND_NON-DOMAIN_NETWORKS"></span>禁止域和非域网络之间的互连

默认情况下，Windows 8、 Windows 8.1 和 Windows 10 的情况下，此策略处于关闭状态。 当启用此策略时，Windows 将尝试阻止 PC 在域网络与非域网络之间相互连接。 担心作为攻击点使用多宿主计算机的潜在安全漏洞时，企业管理员可使用它。

当所有网络路由连接到域，或没有连接的网络路由到域时，此策略不会影响系统的行为。

### <a name="span-idmultiplewirelessnetworksspanspan-idmultiplewirelessnetworksspanspan-idmultiplewirelessnetworksspanmultiple-wireless-networks"></a><span id="Multiple_wireless_networks"></span><span id="multiple_wireless_networks"></span><span id="MULTIPLE_WIRELESS_NETWORKS"></span>多个无线网络

很多 Windows 8、 Windows 8.1 或 Windows 10 移动设备将具有外部 Internet 连接提供给他们在任何时候，即使是在自己的企业 Wi-fi 网络的范围。 启用此策略后，用户可以自由地连接到其公共的移动宽带网络或企业的专用的 wi-fi 网络和在它们之间的开关将。 但是，手动连接某个将自动导致另一个立即断开连接。

### <a name="span-idethernetspanspan-idethernetspanspan-idethernetspanethernet"></a><span id="Ethernet"></span><span id="ethernet"></span><span id="ETHERNET"></span>Ethernet

因为 Windows 8、 Windows 8.1 或 Windows 10 不能自动连接或断开连接到 PC 的以太网电缆，它可以仅以强制实施策略允许或禁止无线连接。 当 PC 具有以太网连接到域网络时，不能连接未连接到域的无线网络，反之亦然。 尝试执行此操作将导致以下错误：

![自动连接管理错误](images/mb-acm-1.png)

对于具有多个以太网端口的电脑，Windows 不能防止通过以物理方式连接到两个不同的以太网网络的 PC 创建相互连接。

### <a name="span-ideffectonsoftdisconnectspanspan-ideffectonsoftdisconnectspanspan-ideffectonsoftdisconnectspaneffect-on-soft-disconnect"></a><span id="Effect_on_soft_disconnect"></span><span id="effect_on_soft_disconnect"></span><span id="EFFECT_ON_SOFT_DISCONNECT"></span>对软影响断开连接

由于禁止互连是一种安全措施，符合此策略的任何断开连接将立即生效，即使没有正在进行的活动。 公共和公司网络之间转换时即使两个网络重叠的用户将遇到连接中断。

例如，使用便携式计算机停靠到公司的以太网连接中参与在移动宽带网络 VoIP 呼叫的用户将丢失调用，尽管应用程序可能会无法通过新的连接会自动恢复。 如果未启用该策略，Windows 会改为软-移动宽带连接断开的连接等待调用完成。 另一方面，停靠到公司网络，因为这两个网络连接到域时也不会中断通过公司的 Wi-fi 网络启动的 VoIP 调用。 在调用完成后，已断开连接的 Wi-fi 网络。

### <a name="span-idprohibitroamingonmobilebroadbandnetworksspanspan-idprohibitroamingonmobilebroadbandnetworksspanspan-idprohibitroamingonmobilebroadbandnetworksspanprohibit-roaming-on-mobile-broadband-networks"></a><span id="Prohibit_roaming_on_mobile_broadband_networks"></span><span id="prohibit_roaming_on_mobile_broadband_networks"></span><span id="PROHIBIT_ROAMING_ON_MOBILE_BROADBAND_NETWORKS"></span>禁止在移动宽带网络上漫游

此策略会阻止 Windows 连接到处于漫游状态的移动宽带网络。 默认情况下，禁用此策略，并且用户可能选择在漫游时手动连接到移动宽带网络或启用自动连接到此类网络。 启用时，则用户无法从连接管理器中选择漫游的移动宽带网络。

## <a name="span-idnetworkpreferencesspanspan-idnetworkpreferencesspanspan-idnetworkpreferencesspannetwork-preferences"></a><span id="Network_preferences"></span><span id="network_preferences"></span><span id="NETWORK_PREFERENCES"></span>网络首选项


在考虑其维护多个连接时，Windows 将使用特征的数来确定首选的网络。 这使用仅在确定是否维护与给定的接口，不适用于路由的连接时。 如果已连接的接口的过程中不是在软断开连接，但路由由路由表中的指标。 如果未手动指定的路由跃点数，则 Windows 会自动将分配基于链接速度的适配器的路由跃点数。

### <a name="span-idconnectionprioritiesspanspan-idconnectionprioritiesspanspan-idconnectionprioritiesspanconnection-priorities"></a><span id="Connection_priorities"></span><span id="connection_priorities"></span><span id="CONNECTION_PRIORITIES"></span>连接优先级

Windows 对划定优先级连接按以下顺序：

1.  以太网网络

2.  当前用户会话期间手动连接网络

3.  连接到 Internet 和 PC 加入的 Active Directory 域的网络

4.  当前连接的 Wi-fi 网络的信号强度

5.  PC 的首选的网络列表

即使链接速度会影响在当前连接的接口之间的路由行为，Windows 将不进行基于链接速度或吞吐量的网络连接决策。 不能配置 Windows 以更改其移动宽带网络和基于当前的移动宽带网络速度的 Wi-fi 网络之间的连接首选项。 如果已连接，用户或桌面应用程序可以更改路由指标来影响路由首选项。

### <a name="span-idsignalstrengthspanspan-idsignalstrengthspanspan-idsignalstrengthspansignal-strength"></a><span id="Signal_strength"></span><span id="signal_strength"></span><span id="SIGNAL_STRENGTH"></span>信号强度

如果 Windows 检测到当前连接的 Wi-fi 网络具有非常低的信号强度，它可能会选择的移动宽带网络连接 （如果策略允许） 以避免中断网络连接。 这有助于顺利转换时用户摆脱无线访问点。

Windows 不会断开更适合的 Wi-fi 网络，直到信号强度不能保持连接。 如果信号强度增加，Windows 可能软-断开连接的移动宽带适配器。

### <a name="span-idpreferrednetworklistspanspan-idpreferrednetworklistspanspan-idpreferrednetworklistspanpreferred-network-list"></a><span id="Preferred_network_list"></span><span id="preferred_network_list"></span><span id="PREFERRED_NETWORK_LIST"></span>首选的网络列表

在大多数情况下，首选的网络列表确定 Windows 将用于连接的无线网络配置文件。 之前 Windows 8 中，此应用于仅使用 Wi-fi 网络的列表。 在 Windows 8、 Windows 8.1 和 Windows 10 中，它还可以包括移动宽带网络。

### <a name="span-idautomaticgenerationspanspan-idautomaticgenerationspanspan-idautomaticgenerationspanautomatic-generation"></a><span id="Automatic_generation"></span><span id="automatic_generation"></span><span id="AUTOMATIC_GENERATION"></span>自动生成

Windows 8、 Windows 8.1 和 Windows 10 自动更新基于用户操作的首选的网络列表。 任何手动连接或断开连接，以便相同的行为会在将来自动发生更新的网络列表。

下面的用户操作修改的首选的网络列表：

-   **最初连接到网络**到网络列表添加新网络。 用户指定自动将在将来连接网络。

    -   第一次连接到新的 Wi-fi 网络使网络优先级最高的网络列表中。

    -   第一次连接到新的移动宽带网络使网络优先级最低的网络列表中。

-   **手动连接到 Wi-fi 网络**列表中较高位置的范围中的任何其他的 Wi-fi 网络移动新连接的网络列表中的下方。 用户指定网络会自动在将来连接。

-   **从网络断开连接**Windows 将不会自动连接到此网络在将来。 将其保留在网络列表在用户修改此设置在将来的情况下。

### <a name="span-idgrouppolicyspanspan-idgrouppolicyspanspan-idgrouppolicyspangroup-policy"></a><span id="Group_Policy"></span><span id="group_policy"></span><span id="GROUP_POLICY"></span>组策略

Wi-fi 配置文件创建的组策略是在网络列表的顶部。 用户可能会手动断开与这些网络连接或手动连接到其他网络，但这些网络保留在网络列表，直到删除的组策略的最高位置。

### <a name="span-idcarrier-provisioningmetadataspanspan-idcarrier-provisioningmetadataspanspan-idcarrier-provisioningmetadataspancarrier-provisioning-metadata"></a><span id="Carrier-provisioning_metadata"></span><span id="carrier-provisioning_metadata"></span><span id="CARRIER-PROVISIONING_METADATA"></span>运营商预配的元数据

移动宽带和 Wi-fi 热点运营商向 Windows 提供一系列的移动宽带和 Wi-fi 配置文件使用[ **ProvisioningAgent** ](https://msdn.microsoft.com/library/windows/apps/br207397)或[ **msProvisionNetworks** ](https://msdn.microsoft.com/library/hh848316) Api。

如果最初预配运算符创建配置文件添加到顶部 (仅限于 Wi-fi) 或现有的网络列表的底部 （如果移动宽带包含）。 您不能影响它们在网络列表中预配的网络的位置。 但是，您可以在网络列表中定义其网络的相对顺序。

用户的操作可能会修改应用程序的预配的元数据之间的网络列表。 当预配的元数据会重新应用时，你所需的网络顺序还原。 但是，重新排序后的一组网络移动到用户已移动到你的网络的任何最低的位置。

在预配的元数据中的网络之间的首选项由以下决定：

1.  每个网络配置文件中的可选优先级属性

2.  媒体类型 （Wi-fi 是更适合移动宽带相比）

3.  XML 文件中指定的顺序

### <a name="span-idmanualmodificationspanspan-idmanualmodificationspanspan-idmanualmodificationspanmanual-modification"></a><span id="Manual_modification"></span><span id="manual_modification"></span><span id="MANUAL_MODIFICATION"></span>手动修改

在 Windows 8 之前的 Wi-fi 首选网络列表是通过管理无线网络控件面板用户可以访问。 遥测指示极少数用户曾经访问此功能。 此外，此用户界面只是为绑定到的 Wi-fi 和可能不包含 Wi-fi 和移动宽带之间的首选项。

大多数用户不需要手动修改网络列表。 但是，某些用户或应用程序可能会发现它需要执行此操作。

### <a name="span-iduserinterfacespanspan-iduserinterfacespanspan-iduserinterfacespanuser-interface"></a><span id="User_interface"></span><span id="user_interface"></span><span id="USER_INTERFACE"></span>用户界面

若要在范围时，请从首选的网络列表中删除配置文件，右键单击网络，然后选择**忘记此网络**。 无法通过用户界面列表从删除不在范围内的网络。

### <a name="span-idwin32apisspanspan-idwin32apisspanspan-idwin32apisspanwin32-apis"></a><span id="Win32_APIs"></span><span id="win32_apis"></span><span id="WIN32_APIS"></span>Win32 Api

应用程序可能使用合适的特定于媒体的 API 在网络列表中创建新的配置文件：

-   对于 Wi-fi 网络，请使用[ **WlanSetProfile** ](https://msdn.microsoft.com/library/windows/desktop/ms706795)函数。

-   对于移动宽带网络，请使用[ **IMbnConnectionProfileManager::CreateConnectionProfile** ](https://msdn.microsoft.com/library/windows/desktop/dd430393)方法。

若要修改网络列表的顺序，请使用[ **WcmSetProfileList** ](https://msdn.microsoft.com/library/windows/desktop/hh437598)函数。 我们不建议使用[ **WlanSetProfileList** ](https://msdn.microsoft.com/library/windows/desktop/ms706805)函数，因为它可能会以意外方式干扰移动宽带的配置文件的网络列表中的位置。

若要从网络列表中删除配置文件，使用相应的特定于媒体的 API:

-   对于 Wi-fi 网络，请使用[ **WlanDeleteProfile** ](https://msdn.microsoft.com/library/windows/desktop/ms706617)函数。

-   对于移动宽带网络，请使用[ **IMbnConnectionProfile::Delete** ](https://msdn.microsoft.com/library/windows/desktop/dd430396)方法。

### <a name="span-idcommand-linespanspan-idcommand-linespanspan-idcommand-linespancommand-line"></a><span id="Command-line"></span><span id="command-line"></span><span id="COMMAND-LINE"></span>Command-line

用户或脚本可能会创建新配置文件在网络列表中通过使用适当的特定于媒体的命令：

-   对于 Wi-fi 网络，请使用**netsh wlan 添加配置文件**命令。

-   对于移动宽带网络，请使用**netsh mbn 添加配置文件**命令。

可以使用修改的网络列表中的 Wi-fi 配置文件顺序**netsh wlan 设置 profileorder**命令。 但是，这不建议，并且可以以意想不到的方式打扰的移动宽带的配置文件列表中的位置。

若要从网络列表中删除配置文件，使用适当的特定于媒体的命令：

-   对于 Wi-fi 网络，请使用**netsh wlan 删除配置文件**命令。

-   对于移动宽带网络，请使用**netsh mbn 删除配置文件**命令。

### <a name="span-idconflictresolutionspanspan-idconflictresolutionspanspan-idconflictresolutionspanconflict-resolution"></a><span id="Conflict_resolution"></span><span id="conflict_resolution"></span><span id="CONFLICT_RESOLUTION"></span>冲突解决方法

如果多个配置文件有相同的网络，Windows 8 和 Windows 8.1 使用以下逻辑来确定应使用哪个配置文件：

1.  **配置文件类型**

    1.  组策略配置文件是首选的用户创建配置文件上。

    2.  单用户配置文件上，所有用户配置文件是首选的。

2.  **接口到达**将使用最近安装的接口上的配置文件。

 

 





