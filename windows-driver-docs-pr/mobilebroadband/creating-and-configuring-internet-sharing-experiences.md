---
title: 创建和配置 Internet 共享体验
description: 创建和配置 Internet 共享体验
ms.assetid: 11906ee4-68f5-4be6-a3ab-6af3253c8a11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02012ea3e6f7b39908a02d6a35df8adc099c3c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383774"
---
# <a name="creating-and-configuring-internet-sharing-experiences"></a>创建和配置 Internet 共享体验


Internet 共享，通常称为 tethering，已添加在 Windows 8.1，若要使用户能够与要为非移动的一个或多个其他设备共享他们的移动宽带网络连接宽带支持。 传统 tethering 机制包括 Bluetooth 和 USB。 但是，Wi-fi 可以提供快速并轻松共享机制，例如个人热点，移动热点，等，因为它需要一些配置的移动宽带连接实现高速数据传输，依赖于熟悉的 Wi-fi连接过程。

Windows 8.1 和 Windows 10 扩展 Internet 通过使客户能够打开并连接到的 Internet 共享配置，电脑通称为 tethering 访问点，就像它是标准的 Wi-fi 网络共享功能进一步。

## <a name="span-idturnoninternetsharingspanspan-idturnoninternetsharingspanspan-idturnoninternetsharingspanturn-on-internet-sharing"></a><span id="Turn_on_Internet_Sharing"></span><span id="turn_on_internet_sharing"></span><span id="TURN_ON_INTERNET_SHARING"></span>打开 Internet 共享


Internet 共享可以打开在移动宽带支持的设备上使用设置超级按钮。 Internet 共享启用后，可以连接到 Wi-fi 网络的任何设备可以连接到它。

**若要打开 Internet 共享**

1.  从**设置**超级按钮，单击**更改电脑设置**，然后单击**网络**。

2.  下**移动宽带**标题下方，单击网络名称。

3.  上**移动宽带**页上，为网络启用 Internet 共享。 如果移动宽带网络断开连接，设备将自动连接到移动宽带网络之前设置的 Wi-fi 网络。

4.  如果已创建必要的服务元数据包，PC 将触发事件告诉 Microsoft Store 移动宽带应用程序运行权利检查。 PC 等待移动宽带的应用，以响应之前启用 Internet 共享。 有关创建服务元数据包的详细信息，请参阅[用于创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

5.  移动宽带网络处于开启状态和任何所需的授权检查已通过后，移动宽带连接是通过使用自定义的网络名称与使用 Wi-Fi Direct 自治组所有者模式的专用的 Wi-fi 网络共享。 这可确保任何 Wi-fi 设备可以连接到网络。

    **请注意**  移动宽带网络的图标会自动更新在整个 Windows 以帮助客户请记住，其他人共享网络。

     

6.  Internet 共享已开启后, 从**移动宽带**页上，单击**编辑**若要更改的网络名称和密码。

    -   Wi-fi 网络必须使用 WPA2-PSK。

    -   网络名称设置为默认值为*&lt;设备名称&gt; &lt;4 位数字&gt;*。 默认的网络名称进行了优化，以确保名称容易识别的用户通过足够短而无法完全适合在网络列表中，足够唯一，以区分多个设备。

    -   密码设置为默认值为 12 个随机数字。

    -   密码必须是长度至少为 8 个字符。

    -   网络名称或密码发生更改时，将重新启动的 Wi-fi 网络。

当打开 Internet 共享时，将发生以下情况：

-   客户端设备上的网络将自动设置为按流量计费的连接以减少不必要的带宽消耗移动宽带网络上。 这可通过使用 Windows 8 特定于供应商信息元素中定义的网络成本的 Wi-fi 信号/探测响应帧。 在 Windows 8.1 中的 Wi-fi 信号/探测响应帧中的元素已添加的另一个特定于供应商的信息通知客户端设备，如果网络是 tethering 网络。 此添加会影响 Windows 8.1 和 Windows 10。

-   当启用 Internet 共享后时，PC 不能进入连接待机或休眠，以确保客户端设备不会丢失其 internet 连接。

-   您可以看到数据已使用客户端设备使用移动宽带应用。

-   最后一台客户端设备具有受限网络断开连接后，Internet 共享将等待五分钟。 如果没有其他客户端设备连接，Internet 共享处于关闭状态，并在 PC 返回到正常电源状态。

-   企业管理员可以禁用 Internet 共享，通过使用组策略。

## <a name="span-idconnecttoatetherednetworkspanspan-idconnecttoatetherednetworkspanspan-idconnecttoatetherednetworkspanconnect-to-a-tethered-network"></a><span id="Connect_to_a_tethered_network"></span><span id="connect_to_a_tethered_network"></span><span id="CONNECT_TO_A_TETHERED_NETWORK"></span>连接到受限网络


您可以连接到受限网络使用的 Wi-fi 设备连接到任何其他的 Wi-fi 网络的方式相同。 但是，如果用户连接到包含这两个运行 Windows 8.1 或 Windows 10 的设备上的相同 Microsoft 帐户凭据的受限网络，则发生以下情况：

-   Internet 共享未打开的 Windows 8.1 或 Windows 10 设备连接时，如果两个设备创建的蓝牙连接并启用 Internet 共享。

-   连接会自动通过自动从受限网络中检索凭据的配置 （网络名称和 SSID）。

**请注意**  如果它们具有使用蓝牙配对设备用户还可以连接到 tethering 访问点。

 

## <a name="span-idconfigureinternetsharingspanspan-idconfigureinternetsharingspanspan-idconfigureinternetsharingspanconfigure-internet-sharing"></a><span id="Configure_Internet_Sharing"></span><span id="configure_internet_sharing"></span><span id="CONFIGURE_INTERNET_SHARING"></span>配置 Internet 共享


某些移动网络运营商 (Mno) 或移动虚拟网络运营商 (Mvno) 不支持 Internet 共享其在网络上，或它们需要在设置 Internet 共享之前权利检查。 Windows 提供了必要的控件，以确保 Windows 设备符合网络策略。 

若要执行此操作在 Windows 8、 Windows 8.1 或 Windows 10 版本 1803年之前，必须创作服务元数据包，并配置[AllowTethering](allowtethering.md)架构中的元素 ([服务元数据数据包架构参考](service-metadata-package-schema-reference.md)). 有关创建服务元数据包的详细信息，请参阅[用于创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。 有以下三个选项：

-   允许所有客户的 Internet 共享。 （默认值如果未指定服务元数据包中）

-   对于所有客户阻止 Internet 共享

-   允许 Internet 共享的客户后权利检查

若要执行此操作在 Windows 10，版本 1803年和更高版本，必须设置[**热点**COSA 数据库中设置](desktop-cosa-apn-database-settings.md#desktop-cosa-only-settings)为适当的值。

如果你决定不需要权利检查，不需要任何其他信息或功能。 如果需要权利检查，则还必须提供背景通知事件处理程序 UWP 移动宽带应用的一部分。 在 Windows 10，版本 1803年和更高版本，使用中的方法[TetheringEntitlementCheckTriggerDetails](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.tetheringentitlementchecktriggerdetails)类来处理 Windows 通知事件，用于检查 tethering 权利。 对于早期版本的 Windows，使用[ **NetworkOperatorNotificationEventDetails** ](https://msdn.microsoft.com/library/windows/apps/br207377)类。 有关创建背景通知事件处理程序的详细信息，请参阅[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

MOs 和 Mvno 具有不同的要求 PDP 上下文应进行 Internet 共享。 Windows 已更新的现有[预配的 XML 架构](https://msdn.microsoft.com/library/windows/apps/hh868398)以允许用户预配系统使用正确的 Internet 共享 PDP 上下文信息。 有关多个 PDP 上下文的详细信息，请参阅[开发应用程序使用多个 PDP 上下文](developing-apps-using-multiple-pdp-contexts.md)。

你还可以配置最大并发连接的客户端设备数量为 10。 您可以更改此数字为任何值介于 3 到 10 之间通过使用[帐户预配](account-provisioning.md)。

为了帮助确保你的用户不会意外地运行对其数据，可以显示数据使用情况统计信息为共享和非共享流量客户移动宽带应用程序中使用[ **GetNetworkUsageAsync**](https://msdn.microsoft.com/library/windows/apps/dn266073)的方法[ **ConnectionProfile** ](https://msdn.microsoft.com/library/windows/apps/br207249)类。

## <a name="span-idcreateacustominternetsharingappspanspan-idcreateacustominternetsharingappspanspan-idcreateacustominternetsharingappspancreate-a-custom-internet-sharing-app"></a><span id="Create_a_custom_Internet_Sharing_app"></span><span id="create_a_custom_internet_sharing_app"></span><span id="CREATE_A_CUSTOM_INTERNET_SHARING_APP"></span>创建自定义的 Internet 共享应用


对于大多数运算符，Windows 用户界面将提供最佳体验的 Internet 共享。 但是，若要在其所有设备和硬件之间创建一致的体验，可以选择要包含在你的移动宽带应用或其他应用程序，它已被授予的特权的访问移动宽带的自己 Internet 共享的用户体验设备。 Windows 提供了几个新 Api 中的[ **Windows.Networking.NetworkOperators 命名空间**](https://msdn.microsoft.com/library/windows/apps/br241148)若要启用您的应用程序执行以下操作：

-   确保系统能够 Internet 共享

-   打开和关闭 Internet 共享

-   查询和配置的 Wi-fi SSID 和网络的通行短语

-   运行权利检查

-   查询的连接的设备数以及连接的设备允许的最大数目

-   接收并响应中的 Internet 共享状态或连接的设备数量的更改通知

 

 





