---
title: 移动宽带概述
description: 移动宽带概述
ms.assetid: 5193927b-7367-468e-8012-c41f6bd743a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e86b91d4f39eac187b8a7a77550f4848d7af16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347477"
---
# <a name="overview-of-mobile-broadband"></a>移动宽带概述


Windows 8、 Windows 8.1 和 Windows 10 简化移动宽带连接的用户，同时提供面向移动网络运营的新机会。 用户体验简化、 一致的连接流。 Windows 8、 Windows 8.1 和 Windows 10 减少您需要开发传统连接管理应用，以便开发资源可以专注客户交互，包括帐户管理和实现增值服务。

Windows 8、 Windows 8.1 和 Windows 10 提供重新构思和简化现有的移动宽带生态系统的机会。

-   早期版本的移动宽带硬件的要求自定义 Windows 驱动程序。 与当前移动宽带类驱动程序，已认证的移动宽带设备具有一致的体验，而无需安装自定义驱动程序。 此简化提供了向客户提供"正常工作"体验，同时可能降低支持开销的机会。

-   自定义的连接管理体验 Windows 功能的功能，并且具有不同的用户体验模型与 Windows 其余部分。 这些连接管理器必须进行部署和维护由运算符和 ISV 合作伙伴。

-   需要自定义驱动程序和自定义连接管理软件的目的是基于 USB 的移动宽带设备需要才能将该自定义软件交付至用户的 PC 上也执行 USB 存储函数。 这一双模式设备概念通常要求用户存储模式和调制解调器模式下，用户可以成功连接到网络之前将添加一个额外的任务之间进行切换。

-   突出显示唯一服务和功能，使您的客户体验唯一。 Windows 8、 Windows 8.1 和 Windows 10 上的客户连接提供机会专注于并以突出显示你的唯一值-通过添加 UWP 移动宽带应用程序，以前称为移动运营商应用程序。

## <a name="span-idkeyscenariosspanspan-idkeyscenariosspanspan-idkeyscenariosspankey-scenarios"></a><span id="Key_scenarios"></span><span id="key_scenarios"></span><span id="KEY_SCENARIOS"></span>关键方案


本部分介绍是您可以选择启用的当前移动宽带体验的一部分的关键方案。 规划您的应用程序必须与进行交互的 Windows 组件时，请考虑每个方案的业务模型的上下文。

-   [计划购买](#plan-purchase)

-   [连接活动设备](#connecting-an-active-device)

-   [运营商通知和系统事件](#operator-notifications-and-system-events)

-   [提供准确的使用情况和计划数据](#providing-accurate-usage-and-plan-data)

-   [Internet 共享](#internet-sharing)

-   [Wi-fi 热点身份验证](#wi-fi-hotspot-authentication)

-   [向用户显示帐户信息](#displaying-account-information-to-the-user)

-   [启用其他设备和应用方案](#enabling-other-devices-and-app-scenarios)

### <a name="plan-purchase"></a>计划购买

无缝计划购买体验使用户更轻松地购买连接，并使操作员能够接受新客户无需支持或零售商店干预。 有两种购买计划选项：

-   移动宽带 PC 上已安装应用程序和服务的元数据。 这可能造成的嵌入了其中 OEM 具有预加载的移动宽带应用，在 Windows 映像或备用的 Internet 连接上的服务元数据是可用的移动宽带硬件的电脑。

-   移动宽带 PC 上未安装应用程序和服务的元数据。 当您插入硬件硬件保护装置和备用的 Internet 连接不可用时，可能发生这种情况。

计划购买选项，无论有根据的 SIM 或 CDMA 移动宽带设备状态的各种子状态。 冷 SIMs （没有关联计划），暖 SIMs （准备好接受一个计划），并在热 SIMs （已与某一计划活动） 有可能呈现基于你想要构建的采购流程是不同的体验。

### <a name="span-idmobilebroadbandappisalreadyinstalledoranalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisalreadyinstalledoranalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisalreadyinstalledoranalternateinternetconnectionisavailablespanmobile-broadband-app-is-already-installed-or-an-alternate-internet-connection-is-available"></a><span id="Mobile_broadband_app_is_already_installed_or_an_alternate_Internet_connection_is_available"></span><span id="mobile_broadband_app_is_already_installed_or_an_alternate_internet_connection_is_available"></span><span id="MOBILE_BROADBAND_APP_IS_ALREADY_INSTALLED_OR_AN_ALTERNATE_INTERNET_CONNECTION_IS_AVAILABLE"></span>移动宽带应用已安装或备用的 Internet 连接不可用

在这种情况下，嵌入式的设备、 移动宽带应用和服务元数据是可能已经安装了通过 SIM 在 PC 上之前，用户尝试激活服务。 另一种可能性是该用户尚不具有移动宽带应用，但具有备用的 Internet 连接才能下载应用。 当插入 SIM 将自动执行以下步骤：

1.  移动宽带服务读取国际移动 (IMSI)，对于 GSM 网络、 CDMA 网络提供程序 ID (SID) 或 CDMA 网络的提供程序名称集成电路卡 ID (ICCID)，并生成一组硬件 Id （是 Hwid)。

    **请注意**  此步骤才有必要，如果 OEM 尚未插入 sim 卡并预加载的移动宽带应用和服务元数据。

     

2.  当 PC 连接到 Internet 时，是 Hwid 发送到 Windows 元数据和 Internet 服务 (WMIS)。 WMIS 标识运算符，并返回相应的服务元数据包。

    **请注意**  此步骤才有必要，如果 OEM 尚未插入 sim 卡并预加载的移动宽带应用和服务元数据。

     

3.  Windows 使用的服务元数据来识别并从 Microsoft Store 中检索的移动宽带应用。 应用程序将自动安装。 在 Windows 8.1 和 Windows 10 中，应用程序不会被固定到开始屏幕。

    **请注意**  此步骤才有必要，如果 OEM 尚未插入 sim 卡并预加载的移动宽带应用和服务元数据。

     

4.  在网络列表中 Windows 连接管理器中显示你运算符徽标和名称。 用户可以连接到网络。

5.  Windows 连接管理器尝试连接的服务元数据中使用网络配置文件的配置信息。 下一步取决于连接的结果：

    -   如果初始连接成功和 Internet 连接可用，不会执行任何进一步操作。 用户以前已购买服务，并且具有一个有效的帐户。

    -   如果初始连接成功，但是 Internet 连接不可用，移动宽带应用启动和用户要求为购买计划。

    -   如果初始连接失败，错误代码指示尚未购买网络服务，移动宽带应用启动。 应用程序可以确定适当的响应。 例如，如果错误代码是由于没有连接，该应用程序可能需要通过电话或连接到的备用的 Internet 连接完成购买将用户定向。

    -   如果初始连接失败，错误代码为另一个，Windows 连接管理器会通知用户错误。 移动宽带应用不会启动。

6.  移动宽带应用打开时，应确保编写应用，以便用户可以购买订阅以便与后端计费基础结构的安全连接。 此过程是专用于每个运算符和 Microsoft 未参与购买过程。 应用程序会建立此连接通过有限的移动宽带连接 （即运营商网络需要启用） 或通过备用的 Internet 连接，如 Wi-fi。

7.  计划购买完成后，移动宽带应用生成预配传递给预配代理的文件元数据。 这会配置 Windows 用户已购买的计划有关的信息。

**重要**  上述步骤也适用于连接到的备用的 Internet 连接与 PC 的外部设备。

 

### <a name="span-idmobilebroadbandappisnotinstalledandnoalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisnotinstalledandnoalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisnotinstalledandnoalternateinternetconnectionisavailablespanmobile-broadband-app-is-not-installed-and-no-alternate-internet-connection-is-available"></a><span id="Mobile_broadband_app_is_not_installed_and_no_alternate_Internet_connection_is_available"></span><span id="mobile_broadband_app_is_not_installed_and_no_alternate_internet_connection_is_available"></span><span id="MOBILE_BROADBAND_APP_IS_NOT_INSTALLED_AND_NO_ALTERNATE_INTERNET_CONNECTION_IS_AVAILABLE"></span>移动宽带应用未安装，并且没有备用的 Internet 连接可用

移动宽带等外部设备，硬件硬件保护装置，可以插入到可能没有可用的备用 Internet 连接可能没有安装的移动宽带应用的电脑。 以下步骤介绍如何构建计划购买体验以解决在此方案中的限制：

1.  一旦检测到移动宽带硬件，则 Windows 移动宽带服务读取 IMSI、 ICCID、 提供程序 ID 或提供程序名称，并生成是 Hwid 表示从设备读取的每个值的一组。 Windows 移动宽带服务侦听的移动宽带相关的事件。

2.  当用户单击**Connect**，HWID 值用于按如下所示的 Windows APN 数据库中找到的连接设置：

    -   如果初始连接成功和 Internet 连接可用，不会执行任何进一步操作。 用户以前已购买服务，并且具有一个有效的帐户。

    -   如果初始连接成功，但是 Internet 连接不可用，则用户是转到此 HWID 范围 APN 数据库中指定的 URL。

    -   如果初始连接失败，Windows 连接管理器会通知用户有关的错误。 你的网站应帮助用户购买计划。

3.  用户完成计划购买后，网站会生成预配文件元数据，并将其传递到预配的代理。 这会配置 Windows 用户已购买的计划有关的基本信息。 根据网络结构中，将发生以下情况之一：

    -   用户被授予当前连接上的 Internet 访问。

    -   预配文件包括断开连接，然后重新连接到同一网络或其他网络，它将提供 Internet 访问权限的说明。

    此时，用户处于联机状态。 现在，Internet 连接不可用，Windows 将检测到移动宽带硬件和下载和安装服务元数据和移动宽带应用程序。

4.  计算从 SIM 或移动宽带设备是 Hwid 将发送到 WMIS。 WMIS 标识运算符，并返回相应的服务元数据包。

5.  Windows 使用的服务元数据来识别并从 Microsoft Store 中检索关联的移动宽带应用。 应用会自动安装并注册后台事件。 在 Windows 8.1 和 Windows 10 中，应用会不会自动固定到开始屏幕。 注册后台事件允许应用以执行对本地数据使用情况计数器作出反应，接收运算符短信、 连接到 Wi-fi 热点和处理授权检查等。 有关后台任务的更多详细信息可在[后台任务简介](http://www.microsoft.com/download/details.aspx?id=27411)。

6.  背景事件发生时，该应用必要时，将生成一个更完整的预配文件，并将其传递给预配的代理。 这会配置 Windows 用户已购买的计划有关的信息。

### <a name="connecting-an-active-device"></a>连接活动设备

在具有活动的移动宽带计划的设备附加到一台 PC，体验是类似于购买时，不同之处在于尝试的连接到 Internet 的潜在顾客。 Windows 将启动用于移动宽带的移动宽带应用或连接到移动运营商的网站。 相反，在后台安装应用。

1.  检测到移动宽带硬件时，移动宽带服务读取 IMSI、 ICCID、 提供程序 ID 或提供程序名称，并生成是 Hwid。

2.  当用户单击**Connect**，HWID 值用于查找 Windows APN 数据库中的适当的连接设置。 为活动设备，连接成功和 Internet 连接可用。

3.  此时，用户处于联机状态。 现在，Internet 连接不可用，Windows 将检测移动宽带硬件以及下载并安装的服务元数据和移动宽带应用程序。

Windows 8.1 和 Windows 10 可以连接到运营商网络在 Windows 安装过程中如果具有活动的计划的移动宽带设备连接到 PC。 移动宽带网络会显示在网络列表中在 Windows 安装过程以及 Wi-fi 网络。 与连接活动设备的过程类似，HWID 基于检测到的移动宽带硬件生成，用于定位 Windows APN 数据库中相应的连接设置。

### <a name="operator-notifications-and-system-events"></a>运营商通知和系统事件

为了保留有关其帐户状态通知用户，移动宽带应用需要执行一些活动，即使在用户不与它交互。 这些活动包括对运算符 SMS 或网络启动 USSD 消息，通知用户他们已接近其数据限制，通知用户他们数据的计划已过期，并通知用户其漫游状态的响应。 传入的 SMS 消息可供有权访问在 PC 上的 SMS 功能通过服务元数据包的特权应用程序。

某些 SMS 消息直接来自移动网络运营商，并应通过使用移动宽带应用显示给用户。 当收到运算符 SMS 消息时，移动宽带应用可以调用 toast 通知。

对于运算符不应在最终用户看到的消息，移动宽带应用可以处理这些并采取相应措施。 Windows 通知服务提供了最有效的直接应用通知通道，但 Windows 还支持从移动宽带网络传入的 SMS 和非结构化补充服务数据 (USSD) 通知的使用。

有关处理短信的详细信息可在[开发 SMS 应用](developing-sms-apps.md)。 运营商通知有关的详细信息可在[启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

1.  服务元数据声明移动宽带应用想要访问运营商通知。 创建专用的后台事件，并在安装时运算符通知事件注册应用。

2.  当此应用使用预配的元数据时，它包括所有短信和 USSD 应视为运算符消息的消息的说明。

收到短信或 USSD 消息，移动宽带服务将预配的元数据中提供的说明对消息进行比较。 如果分析规则都已包括在内，移动宽带服务还将解释该消息和更新数据使用情况信息。

如果消息是匹配项，通知系统事件代理来调用该移动宽带应用程序的专用后台事件。 否则，系统事件代理通知调用公共 SMS 事件。

运算符无法为传入的 SMS 消息的响应的移动宽带应用中包括哪些内容的一些示例包括：

-   立即同步当前数据使用情况

-   向用户显示一条通知

-   更新应用程序的动态磁贴

-   更新预配的元数据检索和应用

**请注意**   Windows 8、 Windows 8.1 和 Windows 10 不包括带有操作系统的短信应用程序因此，为了显示 SMS 消息到所需移动宽带应用或第三方 SMS 应用到的操作员提供特许访问权限用户。

 

**请注意**  构建包含短信的移动宽带应用程序支持，才可向最终用户显示通知 UI 文本接收消息时，这可能需要符合法规要求或以特定的最佳实践市场。

 

短信功能可供移动宽带应用程序，被授予特权的访问权限移动网络运营的 UWP 应用，由 PC OEM （如果移动宽带设备嵌入在 PC 中），授予特权访问权限的 UWP 应用或移动宽带设备 IHV （如果移动宽带设备为可移动）。 移动网络运营和 PC OEM （或移动宽带设备 IHV） 指定特权的应用的整个服务元数据。 有关服务元数据的详细信息，请参阅[使用元数据来配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

### <a name="providing-accurate-usage-and-plan-data"></a>提供准确的使用情况和计划数据

Windows 提供了数据使用情况和移动宽带应用可用于描述用户的数据计划的订阅管理器 Api。 移动宽带应用程序可以更新此 API 与不按流量计费计划，以及为从运营商的网络的更新后的数据使用情况计量数据计划大小有关的信息。

Windows 将检查通过使用这些 Api 已设置为用户的数据使用情况信息并更改核心功能的行为。 例如，Windows 更新将仅自动下载关键更新时用户正在使用按流量计费的网络。 使用情况信息，还可以访问的数据使用情况和订阅管理器 Api; 通过第三方应用详细的使用准则目前[上管理连接按流量计费的网络](https://msdn.microsoft.com/library/windows/apps/hh750310)。

下面是移动宽带应用可以利用为了使用户了解他们的数据使用的各种功能的演练。

1.  本地数据计数器估计，使用量的配置文件已更改的 5%以上的用户的数据限制上次更新后的运算符。 此 5%的增量是硬编码，并使移动宽带应用使用的背景事件本身唤醒并对每个 5%增量做出反应。

2.  数据使用情况和订阅管理器是 Windows 组件不跟踪此 5%的使用率增量。 它将通知系统事件代理，以触发中本地的使用情况估计每个 5%的增量将背景事件。

3.  系统事件代理调用的移动宽带应用来处理后台事件。 （其他触发器，例如传入的通知，可能会导致出现此问题。）移动宽带应用程序可以选择要为此调用时执行的操作。

4.  最佳做法是通过从操作员的计费基础结构，以验证用户实际上已经历的使用量检索最新的使用情况信息来处理此事件的应用。 这可能是一个异步操作在网络上，移动宽带应用程序需要能够获取此信息从计费基础结构，操作员的延迟时间做出反应。 如果在数据使用情况跟踪较长的延迟，移动宽带应用程序可以查询本地数据计数器以填充当前时间和最新数据之间的差距。

5.  对运算符的计费基础结构的 web 查询完成后，移动宽带应用可以应用更新预配的元数据描述可返回到 Windows 的最新使用情况信息。

6.  应用程序将发布更新的信息通过数据使用情况和订阅管理器 Api。

7.  Windows 组件和在电脑上的第三方应用程序可以通过访问此使用情况信息[ **Windows.Networking.Connectivity.ConnectionProfile** ](https://msdn.microsoft.com/library/windows/apps/br207249)类。 应用可以相应地调整其行为。 例如，应用可以在按流量计费网络上使用较低质量的视频流。

### <a name="internet-sharing"></a>Internet 共享

移动宽带为用户提供与的连接，只要它们转。 但是，并非每个设备都有移动宽带设备。 Windows 8.1 和 Windows 10 使用户能够通过 Wi-fi 共享他们的移动宽带连接，与朋友和家人使用不同的设备。

客户可以启用 Internet 共享 PC 设置。 它们还可更改 SSID 的 Wi-fi 网络的密码，并查看有多少人正在共享连接。

对于想要在其设备的另一个使用移动宽带连接的客户，Windows 可以更容易。 只需打开网络列表支持 WiFi 的 PC 运行 Windows 8.1 或 Windows 10 上，单击该共享的设备，SSID，然后单击**Connect**。 Windows 将处理所有的设备配置和设备间通信。

下面是可以配置和管理 Internet 共享的工作原理在 Windows 8.1 和 Windows 10 的各种功能的演练。

1.  您可以选择你的客户可以通过上传服务元数据包的自动下载并安装在电脑上使用 Internet 共享。

2.  使用服务元数据，您还可以选择是否移动宽带应用服务，以查看特定客户已购买支持 tethering 的数据计划对运行权利检查。

3.  移动宽带应用将注册后台事件时用户允许 Internet 共享，并指示 Windows 上允许它运行权利检查。

4.  作为预配的元数据的一部分，可以指定哪些 PDP 上下文和 APN 用于共享的数据流量，以及可以共享连接一次的设备的最大数目。

5.  使用更新后的本地数据使用情况 Api，可以创建显示客户的数据量由其他共享其移动宽带连接的设备在移动宽带应用中的一种体验。

有关 Internet 共享的详细信息，请参阅[创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)。

### <a name="wi-fi-hotspot-authentication"></a>Wi-fi 热点身份验证

作为预配的元数据的一部分，移动宽带应用可以描述用户可以进行身份验证使用其运算符提供凭据的热点。 其中可能包括 WISPr 1.0 热点或加密热点使用 EAP-SIM、 EAP-AKA 或其他受支持的 EAP 方法。

Windows 将自动卸载到范围中这些热点上的数据流量。 您可能想要执行此操作以便卸载从手机数据网络到 land 行基于 Wi-fi 位置的网络流量。 在某些情况下，速度或扩大其覆盖范围比该位置的移动电话数据网络可能增加的 Wi-fi 热点。

您还可以使的热点做法不如移动网络，使其可用于移动宽带连接不是可用，但不是用于数据卸载时要使用的 Windows。

### <a name="span-idsetupspanspan-idsetupspanspan-idsetupspansetup"></a><span id="Setup"></span><span id="setup"></span><span id="SETUP"></span>安装程序

-   移动宽带应用会生成包含 Ssid 和身份验证的预配文件 WiFi 热点的机制，用户可以进行身份验证。 这样可避免用户无需手动输入此信息。

-   预配代理分析配置文件，并提供到 Windows 连接管理器中的所需的信息。 可用时，Windows 会自动连接到这些网络。

### <a name="span-idcredentialgenerationspanspan-idcredentialgenerationspanspan-idcredentialgenerationspancredential-generation"></a><span id="Credential_generation"></span><span id="credential_generation"></span><span id="CREDENTIAL_GENERATION"></span>凭据生成

如果移动宽带应用生成，或在连接期间专有的方式检索 WISPr 凭据，预配的元数据包括对应用程序中，而不提供具体的凭据的引用。 如果包含具体的凭据，则跳过此阶段。

1.  中的 Wi-fi 热点的强制网络门户网站包括无线 Internet 服务提供商漫游 (WISPr) 协议从一项挑战。

2.  如果未提供静态的凭据，Windows 连接管理器将通知系统事件代理发生热点身份验证。 否则，Windows 连接管理器将直接继续进行身份验证。

3.  对于专有身份验证方案，系统事件代理调用的移动宽带应用生成的凭据。

4.  应用会生成使用其专有机制的凭据。 这可能是也可能涉及交互使用网络资源，或使用移动宽带接口。 应用程序最终会执行以下操作之一：

    -   **提供凭据**-应用程序可以生成为此网络的凭据，然后将其返回到 Windows 连接管理器。 向使用 WISPr 热点，Windows 连接管理器进行身份验证。

    -   **取消连接**-的 PC 不应连接到此网络。 Windows 连接管理器结束连接。

    -   **取消身份验证**-应用程序已经过身份验证通过使用另一种方法。 Windows 连接管理器将不进行身份验证或断开连接。

    -   **与用户交互**-应用程序进入前台。 当需要用户进行确认时，如支付每个连接热点，选择此选项。 应用程序最终应执行前面列出的操作之一后，才能查询该用户。

### <a name="span-idauthenticationspanspan-idauthenticationspanspan-idauthenticationspanauthentication"></a><span id="Authentication"></span><span id="authentication"></span><span id="AUTHENTICATION"></span>身份验证

由移动宽带的应用程序 （动态 WISPr 凭据） 提供的凭据或以静态方式定义为预配 （静态 WISPr 凭据，EAP 凭据） 的一部分，Windows 为您提供这些凭据到 Wi-fi 热点。

提供对连接配置文件 Windows 连接管理器中的移动宽带应用的配置信息确定如何获取和传递凭据。 中的下一步的步骤概述了交付：

1.  当用户处于范围的 Wi-fi 热点时，Windows 连接管理器会回复以静态方式定义通过使用预配的元数据的凭据。 移动宽带应用，或通过受信任的网站，可以生成此数据。

2.  Wi-fi 热点运算符验证凭据，然后允许访问 Internet 的 PC。

### <a name="displaying-account-information-to-the-user"></a>向用户显示帐户信息

你可以与你在 Windows 8、 Windows 8.1 和 Windows 10 中的订阅者交互的最佳方式是使用移动宽带应用。 此应用程序开发的可以满足您围绕订阅服务器交互的主要方案。

1.  Windows 确定 MNO 或 MVNO 订阅服务器上属于在 PC 上检测到移动宽带设备时。 运营商的服务元数据匹配，并且使用按 WMIS 下载。

2.  服务元数据链接到相应的网络项 Windows 连接管理器中的移动宽带应用。

3.  Windows 连接管理器显示操作员的徽标，操作员名称和一个**查看我的帐户**链接。

4.  当用户单击该链接时，打开移动宽带应用。 可以开发应用程序以从你的计费系统中检索可用的最新信息。

5.  （可选） 应用程序可以查询的使用情况估计的本地数据计数器，因为上一次更新计费系统。 应用可以使用此数据来显示用户的使用情况的近乎实时的近似值。

6.  更多方案可以到移动宽带应用开发。 有关详细的示例和用户体验的移动宽带应用是否可以启用关键方案的指导原则，请参阅[设计用户体验的移动宽带应用](designing-the-user-experience-of-a-mobile-broadband-app.md)。

### <a name="enabling-other-devices-and-app-scenarios"></a>启用其他设备和应用方案

Windows 8、 Windows 8.1 和 Windows 10 提供了一套丰富的开发工具和灵活的开发平台，你可以利用通过创建突出显示的值的应用程序添加了使之成为唯一的服务。

### <a name="span-idprivilegedappsspanspan-idprivilegedappsspanspan-idprivilegedappsspanprivileged-apps"></a><span id="Privileged_apps"></span><span id="privileged_apps"></span><span id="PRIVILEGED_APPS"></span>特权的应用程序

移动宽带 Api 和界面，包括帐户预配和短信、 仅限于移动宽带应用程序。 必须在 Windows 开发人员中心仪表板提交服务元数据包中声明的特权有权访问这些特权 Api 的应用列表。

### <a name="span-idmultiplepdpcontextsspanspan-idmultiplepdpcontextsspanspan-idmultiplepdpcontextsspanmultiple-pdp-contexts"></a><span id="Multiple_PDP_contexts"></span><span id="multiple_pdp_contexts"></span><span id="MULTIPLE_PDP_CONTEXTS"></span>多个 PDP 上下文

Windows 8.1 和 Windows 10 支持多个 PDP 上下文，同时处于活动状态。 这样，移动运营商向其客户提供不同的方案。 有关使用多个 PDP 上下文启用的方案的详细信息，请参阅[开发应用程序使用多个 PDP 上下文](developing-apps-using-multiple-pdp-contexts.md)。

### <a name="span-idwirelineoperatorsspanspan-idwirelineoperatorsspanspan-idwirelineoperatorsspanwireline-operators"></a><span id="Wireline_operators"></span><span id="wireline_operators"></span><span id="WIRELINE_OPERATORS"></span>有线运算符

PnP X 可用于将非移动宽带设备公开为 UWP 设备应用。

设备，例如 Dvr、 网关路由器、 移动热点和手机可以 （在连接到 Windows 8、 Windows 8.1 或 Windows 10 电脑与相同的 Wi-fi 或 LAN 网络） 使用 PNP-X 让 Windows 8、 Windows 8.1 和 Windows 10 知道它们的存在。 根据属性对其设备的那些设备下载设备元数据并自动下载由你开发的 UWP 设备应用程序。 单个移动宽带应用来管理移动宽带，以及这些其他设备，可以引用此应用程序中的为这些设备。

## <a name="span-idhowitworksspanspan-idhowitworksspanspan-idhowitworksspanhow-it-works"></a><span id="How_it_works"></span><span id="how_it_works"></span><span id="HOW_IT_WORKS"></span>其工作原理


在本部分介绍了 Windows 8、 Windows 8.1 和 Windows 10 中的移动宽带支持关键方案的组件。 它们是 Windows 操作系统的一部分和属于的服务元数据或移动宽带应用之间进行分割。

![组件提供运营商体验](images/mb-overviewtechnicalcomponents.jpg)

### <a name="span-idwindowscomponentsspanspan-idwindowscomponentsspanspan-idwindowscomponentsspanwindows-components"></a><span id="Windows_components"></span><span id="windows_components"></span><span id="WINDOWS_COMPONENTS"></span>Windows 组件

以下组件是 Windows 8、 Windows 8.1 和 Windows 10 的一部分：

-   [预配代理](#provisioning-agent)

-   [数据使用情况和订阅管理器](#data-usage-and-subscription-manager)

-   [Windows 连接管理器](#windows-connection-manager)

-   [本地数据计数器](#local-data-counters)

-   [移动宽带服务](#mobile-broadband-service)

-   [移动宽带类驱动程序](#mobile-broadband-class-driver)

-   [系统事件代理](#system-event-broker)

-   [Windows 元数据和 Internet 服务](#windows-metadata-and-internet-services)

-   [Microsoft 官方商城](#microsoft-store)

### <a name="provisioning-agent"></a>预配代理

预配代理提供了一个接口供你使用你的网络设置配置 Windows。 预配代理将接受一个 XML 文件，描述所需的配置。

可以通过以下方式之一提供的 XML 文件：

-   为网站提供的已签名的 XML 文件[ **window.external.msProvisionNetworks** ](https://msdn.microsoft.com/library/hh848316)函数至少运行的 Windows 8、 Windows 8.1 或 Windows 10 计算机上 Internet Explorer 10 （或另一个支持浏览器）。

-   XML 文件 （无论是有符号或无符号） 提供的应用程序[ **Windows.Networking.NetworkOperators.ProvisioningAgent.ProvisionFromXmlDocumentAsync** ](https://msdn.microsoft.com/library/windows/apps/br207400)函数。

有关格式和预配的文件的内容的更多详细信息，请参阅[使用元数据来配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

### <a name="data-usage-and-subscription-manager"></a>数据使用情况和订阅管理器

数据使用情况和订阅管理器跟踪有关的详细信息的用户的帐户。 有关当前连接的网络的存储的成本信息可供所有 UWP 应用。 可以通过使用预配代理更新此信息。

如果运营商请求它、 数据使用情况和订阅管理器使用本地数据计数器来触发后台事件 5%的数据限制时使用了。 此背景事件的系统事件代理传送和移动宽带应用程序可以使用事件用作触发器来更新可计费使用情况。

### <a name="windows-connection-manager"></a>Windows 连接管理器

Windows 连接管理器监视 Wi-fi、 移动宽带和以太网之间的可用网络。 它可以自动连接和断开决策基于可用的网络。 预配代理可以定义属于您的网络之间的相对优先级。 但是，用户可以手动连接到任何网络。 Windows 连接管理器使用用户的手动操作来影响将来自动连接选项。

Windows 连接管理器还管理后连接支持 WISPr 1.0 的 Wi-fi 热点的身份验证。 如果已存储的 Wi-fi 热点的静态凭据，Windows 连接管理器将自动身份验证。 如果需要动态凭据，Windows 连接管理器通过使用系统事件代理触发后台事件。 移动宽带应用应生成相应的凭据，然后将其交付到 Windows 连接管理器以完成身份验证过程。 有关更多详细信息，请参阅[集成 Windows 与无线热点](integrating-windows-with-wireless-hotspots.md)。

### <a name="local-data-counters"></a>本地数据计数器

本地数据计数器的网络接口上发送和接收的数据量跟踪随着时间的推移。 向多个位置中的用户显示此信息：

-   **应用程序历史记录**选项卡在任务管理器

-   （可选）Windows 连接管理器中的 Wi-fi 或移动宽带网络的扩展视图。 用户可以决定是否要显示或隐藏特定网络此估计值。 默认情况下，它是移动宽带网络显示和隐藏的 Wi-fi 网络。 但是，如果 Windows 检测到安装了移动宽带设备，它会隐藏估计的数据使用情况 Windows 连接管理器中为相应的移动宽带网络。 这是因为已假定，如果已创建移动宽带应用，你将想要控制向用户显示的数据使用情况值。 执行此操作的最佳位置是在移动宽带应用程序。 用户可以选择重写此行为，并在任何时间显示为网络使用情况估计。

本地数据计数器也有以编程方式通过使用以下 Api:

-   [ **Windows.Networking.Connectivity.ConnectionProfile.GetNetworkUsageAsync** ](https://msdn.microsoft.com/library/windows/apps/dn266073)函数指定的时间段内提供的数据使用情况。

-   [ **Windows.Networking.Connectivity.ConnectionProfile.GetConnectivityIntervalsAsync** ](https://msdn.microsoft.com/library/windows/apps/dn266071)函数提供的连接时间戳和网络接口使用时的持续时间。

本地数据使用情况信息用作估计值和用户的指南。 Windows 不能共享相同的数据限制其他设备上的帐户未出单流量或使用情况。 例如，系列计划在不同设备上使用相同的 sim 卡。 移动宽带应用程序应使用本地数据计数器仅以与你的计费系统在上次同步后估计使用情况。 对于已处理的数据使用情况，计费系统应将视为权威标准。

### <a name="mobile-broadband-service"></a>移动宽带服务

移动宽带服务是用于管理移动宽带 Api 和移动宽带设备之间的通信的 Windows 服务。 该服务可以与任何移动宽带设备，其驱动程序符合 Windows 移动宽带驱动程序模型进行交互。

服务还读取新插入的设备的 SIM 和检索服务元数据的进程以及对应于连接的移动宽带设备的移动宽带应用将启动。

### <a name="mobile-broadband-class-driver"></a>移动宽带类驱动程序

移动宽带类驱动程序减少了设备制造商提供其特定的移动宽带设备的自定义驱动程序的负担。 任何移动宽带接口表现为 USB 设备并符合与 USB 实现论坛 (USB-如果) 网络控制模型 (NCM) 2.0 规范将由移动宽带类驱动程序，不需要其他驱动程序为下载或安装。

移动宽带类驱动程序符合 Windows 移动宽带驱动程序模型，并提供到移动宽带服务的完整功能。 它还支持自定义扩展，将直接向移动宽带应用公开。 有关详细信息，请参阅[移动运营商硬件概述](mobile-operator-hardware-overview.md)。

### <a name="system-event-broker"></a>系统事件代理

系统事件代理管理后台事件。 应用，包括移动宽带应用中，可以注册以接收背景事件以响应系统状态中的更改。 可能是移动宽带应用感兴趣的事件包括：

-   **网络状态更改**– 网络连接或断开连接或网络上更改 Internet 连接。

-   **帐户状态更改**– 最终计费周期或 5%的估计数据使用情况的增量。

-   **Wi-fi 热点的身份验证**– 尝试连接到公共 Wi-fi 热点和凭据所需。

-   **传入的运算符通知**– SMS/USSD 消息相匹配某些分析规则，用于描述 SMS/USSD 作为来自运算符。

-   **传入的 SMS** -短信收到与定义运算符的语法分析规则不匹配。

-   **传入 USSD** – USSD 消息收到与定义运算符的语法分析规则不匹配。

开发人员应注意一个严格的限制位于处于不活动状态时，应用可能会占用的 CPU 时间量。 尽管对于某些事件放宽了这些限制，应用始终必须最小化或系统处于低功耗状态时运行另一个应用时它们占用的资源。 有关 Windows 8 和 Windows 10 中的背景事件的详细信息，请参阅[后台任务简介](https://go.microsoft.com/fwlink/?linkid=227329)。

### <a name="windows-metadata-and-internet-services"></a>Windows 元数据和 Internet 服务

Windows 元数据和 Internet 服务 (WMIS) 是可以自定义项从参与的 Windows 设备生态系统的第三方传送到 Windows 的基于云的 Windows 服务。 对于移动宽带设备，WMIS 提供服务元数据包。 这提供了 Windows 所需从 Microsoft Store 中检索的移动宽带应用，第一次，允许连接到网络并显示 Windows 连接管理器中的相应的标记元素的基本信息。

### <a name="microsoft-store"></a>Microsoft Store

Microsoft Store 是 UWP 应用传递到 Windows 8、 Windows 8.1 和 Windows 10 电脑的主要方法。 移动宽带应用程序的应用程序包检索从 Microsoft Store，连接设备后，Internet 连接时可用。 应用包自动安装并且可供用户在该点。 在 Windows 8.1 和 Windows 10 中，应用程序现已推出**所有应用**但不是会自动固定到开始屏幕。

有关 UWP 的设备应用程序的详细信息，请参阅[UWP 设备应用](https://msdn.microsoft.com/library/windows/hardware/dn265154)。

**请注意**  虽然企业可以端负载 UWP 应用在某些情况下的，这些将不再重复介绍本文档中。

 

### <a name="span-idoperatormetadataspanspan-idoperatormetadataspanspan-idoperatormetadataspanoperator-metadata"></a><span id="Operator_metadata"></span><span id="operator_metadata"></span><span id="OPERATOR_METADATA"></span>运营商元数据

有关运算符的元数据被提供三种不同方式适用于 Windows 8 和 Windows 10，如下所述。 每个元数据选项针对一组不同的客户。 了解如何传递三种类型的元数据和在每个使用何种信息将帮助您更好地满足你的客户。

运营商元数据的详细信息，请参阅[使用元数据来配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

### <a name="span-idwindowsapndatabasespanspan-idwindowsapndatabasespanspan-idwindowsapndatabasespanwindows-apn-database"></a><span id="Windows_APN_database"></span><span id="windows_apn_database"></span><span id="WINDOWS_APN_DATABASE"></span>Windows APN 数据库

所有 Windows 8、 Windows 8.1 和 Windows 10 电脑上存在 Windows APN 数据库。 通过使用 Windows 更新来帮助确保连接信息的准确性会定期更新数据库。 对数据库的更新正在通过由你的请求提供服务。 APN 数据库有关如何连接到网络，如果遇到移动宽带设备，包括的 APNs 到它应尝试进行连接，如果没有 Internet 连接，则应定向到用户的 URL 向 Windows 提供信息可用。

此信息旨在让客户联机获得的移动宽带设备连接的秒内。 它应使他们能够使用 Web 浏览器立即购买服务或如果它们已购买服务后，立即联机。

有关将更新提交到 Windows APN 数据库的信息，请参阅[COSA/APN 数据库提交](cosa-apn-database-submission.md)。

### <a name="span-idservicemetadataspanspan-idservicemetadataspanspan-idservicemetadataspanservice-metadata"></a><span id="Service_metadata"></span><span id="service_metadata"></span><span id="SERVICE_METADATA"></span>服务元数据

他或她将移动宽带设备连接后，服务元数据被发送到任何用户。 只要用户具有任何形式的 Internet 连接，包括按流量计费的移动宽带或漫游网络始终自动下载服务元数据。

此信息使客户能够通过让你可以添加为 Windows 连接管理器中的标记元素、 引用从 Microsoft Store 中，会自动获取的移动宽带应用并具有最新的移动具有更丰富的体验联机购买或 Internet 连接的宽带设置。 Windows 将定期检查它具有最新的服务元数据包从 WMIS。

仅当在 PC 上检测到从指定的运算符的移动宽带设备时，服务元数据包被发送到客户。 它是存在时，此包中的信息将覆盖 APN 数据库的内容。 服务元数据数据包架构参考的详细信息，请参阅[服务的元数据数据包架构参考](service-metadata-package-schema-reference.md)。

有关如何创建服务元数据包的说明，请参阅[用于创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

### <a name="span-idprovisioningmetadataspanspan-idprovisioningmetadataspanspan-idprovisioningmetadataspanprovisioning-metadata"></a><span id="Provisioning_metadata"></span><span id="provisioning_metadata"></span><span id="PROVISIONING_METADATA"></span>预配的元数据

预配的元数据是由传递到 PC 操作员的网站或移动宽带应用后订阅服务器上已购买服务。 预配的元数据打包为一个 XML 文件，并由预配代理以修改网络设置 PC 的处理。

可以为每个订阅者个人要求指定预配的元数据。 预配的元数据还可能使用更高的频率使用移动宽带应用更新。 在预配的元数据中的信息将覆盖 APN 数据库和服务元数据的内容。 这是因为它往往是有关订阅服务器上的最特定和定制信息。

 

 





