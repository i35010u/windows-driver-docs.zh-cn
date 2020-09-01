---
title: 移动宽带概述
description: 移动宽带概述
ms.assetid: 5193927b-7367-468e-8012-c41f6bd743a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5695896f0aef36edc11d3ef9a758c1bc871de64
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218183"
---
# <a name="overview-of-mobile-broadband"></a>移动宽带概述

Windows 8、Windows 8.1 和 Windows 10 简化了用户的移动宽带连接，同时为移动网络操作员提供了新的机会。 用户享有简单、一致的连接流。 Windows 8、Windows 8.1 和 Windows 10 降低了开发传统连接管理应用程序的需要，因此开发资源可以集中在客户交互上，包括帐户管理和增值服务。

Windows 8、Windows 8.1 和 Windows 10 提供重新构建和精简现有移动宽带生态系统的机会。

- 早期版本的移动宽带硬件要求自定义 Windows 驱动程序。 使用最新的移动宽带类驱动程序，经过认证的移动宽带设备具有一致的体验，无需安装自定义驱动程序。 这种简化为客户提供 "仅工作" 体验的机会，同时可能降低支持开销。

- 自定义的连接管理体验到重复的 Windows 功能，并具有不同于 Windows 其余部分的 UX 模型。 这些连接管理器必须由运营商及其 ISV 合作伙伴部署和维护。

- 自定义驱动程序和自定义连接管理软件的需求意味着，基于 USB 的移动宽带设备还需要执行 USB 存储功能，以便将该自定义软件传递到用户的 PC。 这种双重模式的设备概念通常要求用户在存储模式和调制解调器模式间切换，添加额外的任务后，用户才能成功连接到网络。

- 突出显示使你的客户体验独一无二的独特服务和功能。 Windows 8、Windows 8.1 和 Windows 10 提供了将重点放在客户连接上的机会，并通过 UWP mobile 宽带应用（以前称为移动运营商应用）突出显示独特的价值。

## <a name="key-scenarios"></a>关键方案

本部分介绍了作为当前移动宽带体验的一部分的关键方案，你可以选择启用它。 在规划您的应用程序必须与其交互的 Windows 组件时，请考虑在您的业务模型环境中每个方案。

- [计划购买](#plan-purchase)

- [连接活动设备](#connecting-an-active-device)

- [操作员通知和系统事件](#operator-notifications-and-system-events)

- [提供准确的使用情况和计划数据](#providing-accurate-usage-and-plan-data)

- [Internet 共享](#internet-sharing)

- [Wi-fi 热点身份验证](#wi-fi-hotspot-authentication)

- [向用户显示帐户信息](#displaying-account-information-to-the-user)

- [启用其他设备和应用方案](#enabling-other-devices-and-app-scenarios)

### <a name="plan-purchase"></a>规划购买

无缝计划购买体验使用户能够更轻松地购买连接，使操作员能够在不需要支持或零售商店干预的情况下接受新客户。 有两个采购计划选项：

- 移动宽带应用和服务元数据已安装在电脑上。 对于具有嵌入的移动宽带硬件的电脑，这种情况可能发生，OEM 已在 Windows 映像上预加载移动宽带应用和服务元数据，或者提供备用 Internet 连接。

- 计算机上未安装移动宽带应用和服务元数据。 当插入硬件转换器并且备用 Internet 连接不可用时，可能会发生这种情况。

无论采用哪种计划购买选项，都可以根据 SIM 或 CDMA 移动宽带设备的状态进行各种子状态。 冷 Sim (无相关计划) 、温 Sim (准备接受计划) ，并且已与计划进行活动的热 Sim (可能会根据你想要如何构建购买流程来提供不同的体验。

### <a name="mobile-broadband-app-is-already-installed-or-an-alternate-internet-connection-is-available"></a>已安装移动宽带应用，或者提供备用 Internet 连接

在这种情况下，在用户尝试激活服务之前，嵌入式设备、移动宽带应用和服务元数据可能已安装在具有 SIM 的电脑上。 另一种可能的情况是，用户还没有移动宽带应用，而是通过备用 Internet 连接下载应用。 插入 SIM 后，会自动执行以下步骤：

1. 移动宽带服务读取国际移动用户身份 (IMSI) ，集成卡 ID (ICCID) 用于 GSM 网络，提供程序 ID (SID) 用于 CDMA 网络，或 CDMA 网络的提供程序名称，并生成一组硬件 Id (Hwid) 。

    **注意**   只有 OEM 尚未插入 SIM 并预加载移动宽带应用和服务元数据时，才需要执行此步骤。

2. 当电脑连接到 Internet 时，Hwid 将发送到 Windows 元数据，Internet 服务 (WMIS) 。 WMIS 标识运算符并返回相应的服务元数据包。

    **注意**   只有 OEM 尚未插入 SIM 并预加载移动宽带应用和服务元数据时，才需要执行此步骤。

3. Windows 使用服务元数据从 Microsoft Store 中标识和检索移动宽带应用。 此应用将自动安装。 在 Windows 8.1 和 Windows 10 中，应用未固定到 "开始" 屏幕。

    **注意**   只有 OEM 尚未插入 SIM 并预加载移动宽带应用和服务元数据时，才需要执行此步骤。

4. 操作员徽标和名称出现在 Windows 连接管理器的 "网络" 列表中。 用户可以连接到你的网络。

5. Windows 连接管理器尝试使用服务元数据中的网络配置文件配置信息进行连接。 下一步取决于连接的结果：

    - 如果初始连接成功并且 Internet 连接可用，则无需进一步操作。 用户以前购买过服务，并且具有活动的帐户。

    - 如果初始连接成功，但 Internet 连接不可用，则会启动移动宽带应用，并要求用户提供购买计划。

    - 如果初始连接失败，并且错误代码指示尚未购买网络服务，则表示移动宽带应用程序已启动。 应用可以确定相应的响应。 例如，如果错误代码是由于缺少连接引起的，则应用可能需要指示用户通过电话或通过连接到备用 Internet 连接来完成购买。

    - 如果初始连接失败并出现其他错误代码，则 Windows 连接管理器会将错误通知给用户。 移动宽带应用未启动。

6. 当移动宽带应用打开时，你应该确保编写应用以建立与后端计费基础结构的安全连接，以便用户可以购买订阅。 此过程仅适用于每个操作员，而 Microsoft 不涉及购买过程。 此应用通过有限的移动宽带连接建立此连接 (，操作员网络需要启用) 或通过备用 Internet 连接，如 Wi-fi。

7. 计划购买完成后，移动宽带应用会生成一个传递到预配代理的元数据设置文件。 这会将 Windows 配置为用户已购买的计划的相关信息。

**重要提示**   上述步骤还适用于通过备用 Internet 连接连接到 PC 的外部设备。

### <a name="mobile-broadband-app-is-not-installed-and-no-alternate-internet-connection-is-available"></a>未安装移动宽带应用，且无备用 Internet 连接可用

可以将外部移动宽带设备（如硬件转换器）插入到可能未提供备用 Internet 连接并且可能没有安装移动宽带应用的 Pc 中。 以下步骤说明如何构建计划购买体验来解决此方案中的限制：

1. 一旦检测到移动宽带硬件，Windows Mobile 宽带服务就会读取 IMSI、ICCID、提供程序 ID 或提供程序名称，并生成一组表示从设备读取的每个值的 Hwid。 Windows Mobile 宽带服务侦听移动宽带相关事件。

2. 当用户单击 " **连接**" 时，HWID 值用于在 Windows APN 数据库中查找连接设置，如下所示：

    - 如果初始连接成功并且 Internet 连接可用，则无需进一步操作。 用户以前购买过服务，并且具有活动的帐户。

    - 如果初始连接成功，但 Internet 连接不可用，则会将该用户转到此 HWID 范围的 APN 数据库中指定的 URL。

    - 如果初始连接失败，Windows 连接管理器会将错误通知给用户。 网站应帮助用户购买计划。

3. 在用户完成计划购买后，该网站将生成元数据预配文件并将其传递到预配代理。 这会将 Windows 配置为包含用户已购买计划的基本信息。 根据网络结构，会发生以下情况之一：

    - 用户在当前连接上被授予 Internet 访问权限。

    - 预配文件包含了断开连接并重新连接到同一网络或其他网络（将提供 Internet 访问）的说明。

    此时，用户处于联机状态。 现在 Internet 连接可用，Windows 将检测移动宽带硬件，并下载并安装服务元数据和移动宽带应用。

4. 从 SIM 或移动宽带设备计算的 Hwid 将发送到 WMIS。 WMIS 标识运算符并返回相应的服务元数据包。

5. Windows 使用服务元数据从 Microsoft Store 中标识和检索关联的移动宽带应用。 应用会自动安装并注册到后台事件。 在 Windows 8.1 和 Windows 10 中，应用程序不会自动固定到 "开始" 屏幕。 通过注册后台事件，应用程序可以执行一些操作，如对本地数据使用计数器做出反应、接收操作员短信、连接到 Wi-fi 热点和处理权利检查。

6. 当后台事件发生时，应用程序会生成更完整的预配文件（如果需要），并将其传递给预配代理。 这会将 Windows 配置为用户已购买的计划的相关信息。

### <a name="connecting-an-active-device"></a>连接活动设备

当具有活动移动宽带计划的设备附加到电脑时，体验与购买的体验相似，只不过尝试的连接会导致 Internet。 Windows 不会启动移动宽带应用程序或连接到移动运营商的网站。 而是在后台安装应用程序。

1. 检测到移动宽带硬件后，移动宽带服务将读取 IMSI、ICCID、提供程序 ID 或提供程序名称，并生成 Hwid。

2. 当用户单击 " **连接**" 时，HWID 值用于在 Windows APN 数据库内查找适当的连接设置。 对于活动设备，连接成功并且 Internet 连接可用。

3. 此时，用户处于联机状态。 现在 Internet 连接可用，Windows 将检测移动宽带硬件，并下载并安装服务元数据和移动宽带应用。

如果将具有活动计划的移动宽带设备附加到电脑，Windows 8.1 和 Windows 10 可以在 Windows 安装程序期间连接到操作员网络。 移动宽带网络在 Windows 安装程序和 Wi-fi 网络一起显示在 "网络" 列表中。 与活动设备的连接过程类似，HWID 是根据检测到的移动宽带硬件生成的，并用于在 Windows APN 数据库内查找适当的连接设置。

### <a name="operator-notifications-and-system-events"></a>操作员通知和系统事件

为了使用户了解其帐户状态，移动宽带应用需要执行某些活动，即使用户不与它交互也是如此。 这些活动包括响应操作员短信或网络启动的 USSD 消息，通知用户他们已接近其数据限制，通知用户其数据计划已过期，并通知用户其漫游状态。 传入的 SMS 消息适用于已通过服务元数据包被授权访问 PC 上的 SMS 功能的特权应用。

某些 SMS 消息直接来自移动网络操作员，并应通过使用移动宽带应用显示给用户。 移动宽带应用在收到操作员 SMS 消息时可以调用 toast 通知。

对于最终用户不应查看的操作员消息，移动宽带应用程序可以处理这些消息并进行相应操作。 Windows 通知服务提供了最有效的直接到应用通知通道，但 Windows 也支持使用传入的 SMS 和非结构化补充服务数据 (USSD 从移动宽带网络) 通知。

有关如何处理 SMS 消息的详细信息，请参阅 [开发 sms 应用](developing-sms-apps.md)。 有关操作员通知的详细信息，请参阅 [启用移动运营商通知和系统事件](enabling-mobile-operator-notifications-and-system-events.md)。

1. 服务元数据声明移动宽带应用想要访问操作员通知。 在安装时，将创建一个专用后台事件，并为其注册操作员通知事件。

2. 当应用应用预配元数据时，它包括应视为操作员消息的所有 SMS 和 USSD 消息的说明。

收到短信或 USSD 消息后，移动宽带服务会将消息与预配元数据中提供的说明进行比较。 如果已包含分析规则，则移动宽带服务还会解释该消息，并更新有关数据使用情况的信息。

如果消息是匹配项，则会通知系统事件代理调用该移动宽带应用程序的专用后台事件。 否则，系统事件代理将被通知调用公共 SMS 事件。

用于响应传入 SMS 消息的移动宽带应用程序中可以包含的操作的一些示例包括：

- 立即同步当前数据使用情况

- 向用户显示通知

- 更新应用的动态磁贴

- 检索和应用更新的设置元数据

**注意**   Windows 8、Windows 8.1 和 Windows 10 不会将 SMS 应用程序包含在操作系统中，因此，需要操作员提供的移动宽带应用程序或第三方 SMS 应用程序向用户显示 SMS 消息。

 **注意**   若要在收到文本消息时向最终用户显示通知 UI，则需要构建具有 SMS 支持的移动宽带应用程序，这可能需要满足特定市场的法规要求或最佳做法。

 SMS 功能适用于移动宽带应用、有权访问移动网络操作员的 UWP 应用、有权访问移动网络操作员的 UWP 应用、如果移动宽带设备嵌入到 PC) ，或移动宽带设备 IHV (如果移动宽带设备是) 可移动宽带设备，则为其提供特权访问 (。 移动网络操作员和 PC OEM (或移动宽带设备 IHV) 通过服务元数据指定特权应用。 有关服务元数据的详细信息，请参阅 [使用元数据配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

### <a name="providing-accurate-usage-and-plan-data"></a>提供准确的使用情况和计划数据

Windows 提供了数据使用情况和订阅管理器 Api，mobile 宽带应用可使用该 Api 来描述用户的数据计划。 移动宽带应用可以使用有关数据计划大小、计数与非计量计划的信息以及来自操作员网络的更新数据使用值来更新此 API。

Windows 将检查使用这些 Api 为用户设置的数据使用情况信息并更改核心功能的行为。 例如，仅当用户使用按流量计费的网络时，Windows 更新才会自动下载关键更新。 其他第三方应用程序也可通过数据使用和订阅管理器 Api 访问使用情况信息。

以下是移动宽带应用可选择使用的各种功能的演练，以使用户能够知道其数据使用情况。

1. 本地数据计数器估计，自上次更新后，对配置文件的使用情况已更改，超过用户数据限制的5%。 这5% 的增量是硬编码的，移动宽带应用可以使用后台事件来唤醒自身，并对每5% 的增量做出反应。

2. "数据使用情况" 和 "订阅管理器" 是一种 Windows 组件，用于执行5% 的使用率增量跟踪。 它通知系统事件代理在本地估计使用量内为每5% 增量触发一个后台事件。

3. 系统事件代理调用移动宽带应用程序来处理后台事件。  (其他触发器（如传入通知）可能会导致此情况发生。 ) 移动宽带应用程序可以选择在为此目的调用时要执行的操作。

4. 最佳做法是，通过从操作员的计费基础结构检索最新的使用情况信息来验证该用户实际经历了多少使用量来处理此事件。 这很可能是通过网络的异步操作，并且移动宽带应用程序需要能够对从操作员的计费基础结构获取此信息的延迟做出反应。 如果数据使用量跟踪出现明显的延迟，则移动宽带应用可以查询本地数据计数器，以填充当前时间与最近数据之间的差距。

5. 当对操作员的计费基础结构进行 web 查询时，移动宽带应用程序可以应用更新的预配元数据来描述可返回到 Windows 的最新使用情况信息。

6. 此应用通过数据使用情况和订阅管理器 Api 发布更新后的信息。

7. 计算机上的 Windows 组件和第三方应用程序可以使用 [**ConnectionProfile**](/uwp/api/Windows.Networking.Connectivity.ConnectionProfile) 类访问此使用情况信息。 应用可以相应地调整其行为。 例如，应用可以在按流量计费的网络上使用较低质量的视频流。

### <a name="internet-sharing"></a>Internet 共享

移动宽带为用户提供了随时随地的连接。 但是，并非每个设备都有移动宽带设备。 Windows 8.1 和 Windows 10 使用户能够通过 Wi-fi 与使用不同设备的好友和家人共享其移动宽带连接。

客户可以在 "电脑设置" 中打开 Internet 共享。 它们还可以更改 Wi-fi 网络的 SSID 和密码，并查看共享连接的用户数量。

对于想要在其其他设备上使用移动宽带连接的客户，Windows 使其变得更简单。 只需在运行 Windows 8.1 或 Windows 10 的支持 WiFi 的 PC 上打开网络列表，单击共享设备的 SSID，然后单击 " **连接**"。 Windows 将处理所有设备配置和设备间通信。

下面是可以配置和管理 Internet 共享在 Windows 8.1 和 Windows 10 上的工作方式的各种功能的演练。

1. 可以通过上载自动下载并安装在电脑上的服务元数据包，来选择客户是否能够使用 Internet 共享。

2. 使用服务元数据，你还可以选择移动宽带应用是否对服务运行权利检查，以查看特定客户是否购买了支持 tethering 的数据计划。

3. 移动宽带应用注册后台事件以便在用户启用 Internet 共享时运行权利检查，并指示 Windows 是否允许。

4. 作为预配元数据的一部分，你可以指定要用于共享数据流量的 PDP 上下文和 APN，以及可一次共享连接的最大设备数。

5. 使用更新的本地数据使用情况 Api，你可以在移动宽带应用中创建体验，以向客户显示共享其移动宽带连接的其他设备所使用的数据量。

有关 Internet 共享的详细信息，请参阅 [创建和配置 Internet 共享体验](creating-and-configuring-internet-sharing-experiences.md)。

### <a name="wi-fi-hotspot-authentication"></a>Wi-fi 热点身份验证

作为预配元数据的一部分，移动宽带应用可以描述用户可以使用其操作员提供的凭据进行身份验证的热点。 其中可能包括使用 EAP-SIM、EAP 或其他支持的 EAP 方法的 WISPr 1.0 热点或加密的热点。

在范围内时，Windows 会自动将数据流量卸载到这些热点。 你可能想要执行此操作，以便将网络流量从移动电话数据网络转移到基于土地的 Wi-fi 位置。 在某些情况下，Wi-fi 热点可能会提高速度，或比该位置的移动电话数据网络更好的覆盖范围。

你还可以设置比移动网络更少的热点，使其可供 Windows 在移动宽带连接不可用时使用，但不能用于数据卸载。

### <a name="setup"></a>设置

- 移动宽带应用会生成一个预配文件，其中包含用户可进行身份验证的 WiFi 热点的 Ssid 和身份验证机制。 这样，用户就不必手动输入此信息。

- 预配代理会分析预配文件，并向 Windows 连接管理器提供必需的信息。 当这些网络可用时，Windows 会自动连接到它们。

### <a name="credential-generation"></a>凭据生成

如果移动宽带应用在连接期间以专有方式生成或检索 WISPr 凭据，则设置元数据包括对应用的引用，而不是提供特定凭据。 如果包含特定凭据，则跳过此阶段。

1. Wi-fi 热点中的固定门户网站包括无线 Internet 服务提供商漫游 (的一项挑战) 协议。

2. 如果未提供静态凭据，Windows 连接管理器将通知系统事件代理正在进行热点身份验证。 否则，Windows 连接管理器会直接转到身份验证。

3. 对于专有身份验证方案，系统事件代理调用移动宽带应用以生成凭据。

4. 应用使用其专用机制生成凭据。 这些资源不一定涉及与网络资源的交互，也可能不涉及移动宽带接口。 应用最终会执行以下操作之一：

    - **提供凭据** --该应用可生成此网络的凭据，然后将其返回给 Windows 连接管理器。 Windows 连接管理器使用 WISPr 向热点进行身份验证。

    - **取消连接** --PC 不应连接到此网络。 Windows 连接管理器将结束连接。

    - **取消身份验证** -已使用替代方法对应用进行身份验证。 Windows 连接管理器不会进行身份验证，也不会断开连接。

    - **与用户交互** -将应用程序置于前台。 这是在需要用户确认时选择的，例如，按连接付费的热点。 在咨询用户后，应用应最终获取之前列出的操作之一。

### <a name="authentication"></a>身份验证

如果移动宽带应用提供凭据 (动态 WISPr 凭据) 或静态定义为预配 (静态 WISPr 凭据、EAP 凭据) ，Windows 会将这些凭据传递到 Wi-fi 热点。

移动宽带应用程序向 Windows 连接管理器中的连接配置文件提供的配置信息确定如何获取和传递凭据。 后续步骤中概述了传递：

1. 当用户处于 Wi-fi 热点范围内时，Windows 连接管理器使用预配元数据静态定义的凭据进行回复。 此数据可由移动宽带应用或受信任的网站生成。

2. Wi-fi 热点使用操作员验证凭据，然后允许 PC 访问 Internet。

### <a name="displaying-account-information-to-the-user"></a>向用户显示帐户信息

若要在 Windows 8、Windows 8.1 和 Windows 10 中与订户交互的最佳方式是使用移动宽带应用。 此应用是由你开发的，用于满足订户交互的关键方案。

1. 当在 PC 上检测到移动宽带设备时，Windows 会确定订户所属的 o 或 MVNO。 WMIS 使用匹配和下载该操作员的服务元数据。

2. 服务元数据将移动宽带应用链接到 Windows 连接管理器中相应的网络条目。

3. Windows 连接管理器显示操作员的徽标、操作员名称和 **"查看我的帐户"** 链接。

4. 当用户单击该链接时，将打开移动宽带应用。 可以开发应用来检索计费系统中可用的最新信息。

5. 应用程序可以根据需要查询本地数据计数器，以估计自上次更新计费系统以来的使用情况。 应用可以使用此数据来显示用户使用情况的近乎实时的近似值。

6. 可以在移动宽带应用中开发更多方案。 有关移动宽带应用可以启用的关键方案的详细示例和用户体验准则，请参阅 [设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)。

### <a name="enabling-other-devices-and-app-scenarios"></a>启用其他设备和应用方案

Windows 8、Windows 8.1 和 Windows 10 提供了一组丰富的开发工具和一个灵活的开发平台，你可以通过创建突出显示增值服务的应用，使其保持唯一。

### <a name="privileged-apps"></a>特权应用

移动宽带 Api 和接口（包括帐户预配和 SMS）仅限于移动宽带应用。 必须在提交到 Windows 开发人员中心仪表板的服务元数据包中声明有权访问这些特权 Api 的特权应用列表。

### <a name="multiple-pdp-contexts"></a>多个 PDP 上下文

Windows 8.1 和 Windows 10 支持同时处于活动状态的多个 PDP 上下文。 这允许移动运营商向其客户提供不同的方案。 有关通过使用多个 PDP 上下文启用的方案的详细信息，请参阅 [使用多个 pdp 上下文开发应用](developing-apps-using-multiple-pdp-contexts.md)。

### <a name="wireline-operators"></a>有线操作员

你可以使用 Pnp-x 将非 mobile 宽带设备公开为 UWP 设备应用。

当连接到与 Windows 8、Windows 8.1 或 Windows 10 电脑相同的 Wi-fi 或 LAN 网络时，可以 (设备（如 DVRs、网关路由器、移动热点和手机）) 使用 Pnp-id 使 Windows 8、Windows 8.1 和 Windows 10 知道其存在。 系统会基于设备的设备属性下载设备元数据，并会自动下载设备元数据。 你可以为这些设备引用此应用程序，以便单个移动宽带应用可以管理移动宽带以及这些其他设备。

## <a name="how-it-works"></a>工作原理

本部分介绍了在 Windows 8、Windows 8.1 和 Windows 10 中支持移动宽带关键方案的组件。 它们划分为 Windows 操作系统的一部分，以及作为服务元数据或移动宽带应用程序一部分的部分。

![提供操作员体验的组件](images/mb-overviewtechnicalcomponents.jpg)

### <a name="windows-components"></a>Windows 组件

以下组件是 Windows 8、Windows 8.1 和 Windows 10 的一部分：

- [设置代理](#provisioning-agent)

- [数据使用情况和订阅管理器](#data-usage-and-subscription-manager)

- [Windows 连接管理器](#windows-connection-manager)

- [本地数据计数器](#local-data-counters)

- [移动宽带服务](#mobile-broadband-service)

- [移动宽带类驱动程序](#mobile-broadband-class-driver)

- [系统事件代理](#system-event-broker)

- [Windows 元数据和 Internet 服务](#windows-metadata-and-internet-services)

- [Microsoft Store](#microsoft-store)

### <a name="provisioning-agent"></a>设置代理

预配代理提供了一个接口，用于使用网络设置配置 Windows。 预配代理接受描述所需配置的 XML 文件。

可以通过以下方式之一提供 XML 文件：

- 网站在 Windows 8、Windows 8.1 或 Windows 10 计算机上提供的已签名的 XML 文件 [**，该文件**](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85)) 至少运行 Internet Explorer 10 (或其他支持浏览器) 。

- XML 文件 (应用提供的有符号或无符号) [**windows.networking.networkoperators. ProvisionFromXmlDocumentAsync**](/uwp/api/windows.networking.networkoperators.provisioningagent.provisionfromxmldocumentasync?view=winrt-19041#Windows_Networking_NetworkOperators_ProvisioningAgent_ProvisionFromXmlDocumentAsync_System_String_) 函数。

有关预配文件格式和内容的更多详细信息，请参阅 [使用元数据配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

### <a name="data-usage-and-subscription-manager"></a>数据使用情况和订阅管理器

"数据使用情况" 和 "订阅管理员" 跟踪有关用户帐户的详细信息。 当前连接的网络的存储成本信息可用于所有 UWP 应用。 你可以通过使用预配代理来更新此信息。

如果运营商请求它，则在使用了5% 的数据限制时，数据使用情况和订阅管理器将使用本地数据计数器来触发后台事件。 系统事件代理提供此背景事件，移动宽带应用可以使用事件作为触发器来更新计费使用情况。

### <a name="windows-connection-manager"></a>Windows 连接管理器

Windows 连接管理器跨 Wi-fi、移动宽带和以太网监视可用网络。 它基于可用网络进行自动连接和断开连接决策。 预配代理使你能够定义你拥有的网络之间的相对优先级。 但是，用户可以手动连接到任何网络。 Windows 连接管理器使用用户的手动操作来影响将来的自动连接选择。

Windows 连接管理器还可管理支持 WISPr 1.0 的 Wi-fi 热点的连接后身份验证。 如果为 Wi-fi 热点存储了静态凭据，Windows 连接管理器将自动进行身份验证。 如果需要动态凭据，Windows 连接管理器会使用系统事件代理触发后台事件。 然后，移动宽带应用程序将生成相应的凭据并将其传递给 Windows 连接管理器，以便完成身份验证过程。 有关更多详细信息，请参阅将 [Windows 与无线热点集成](integrating-windows-with-wireless-hotspots.md)。

### <a name="local-data-counters"></a>本地数据计数器

本地数据计数器跟踪一段时间内网络接口上发送和接收的数据量。 此信息向用户显示在多个位置：

- 任务管理器中的 " **应用历史记录** " 选项卡

-  (可以选择在 Wi-fi 或移动宽带网络的展开视图中) Windows 连接管理器。 用户可以决定是显示还是隐藏特定网络的估计值。 默认情况下，它针对移动宽带网络显示，对于 Wi-fi 网络为隐藏状态。 但是，如果 Windows 检测到移动宽带设备已安装，它会在相应移动宽带网络的 Windows 连接管理器中隐藏预计的数据使用量。 这是因为假设你已创建移动宽带应用，则需要控制向用户显示的数据使用值。 要执行此操作的最佳位置是在移动宽带应用程序内。 用户可以选择重写此行为，并随时显示网络的估计使用量。

还可以通过使用以下 Api 以编程方式使用本地数据计数器：

- [**ConnectionProfile. GetNetworkUsageAsync**](/uwp/api/windows.networking.connectivity.connectionprofile.getattributednetworkusageasync?view=winrt-19041#Windows_Networking_Connectivity_ConnectionProfile_GetAttributedNetworkUsageAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_NetworkUsageStates_)函数提供指定时间段内的数据使用情况。

- 使用网络接口时， [**ConnectionProfile. GetConnectivityIntervalsAsync**](/uwp/api/windows.networking.connectivity.connectionprofile.getconnectivityintervalsasync?view=winrt-19041#Windows_Networking_Connectivity_ConnectionProfile_GetConnectivityIntervalsAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_NetworkUsageStates_) 函数提供连接时间戳和持续时间。

本地数据使用情况信息用作用户的估计和指南。 Windows 无法考虑未开票流量或其他共享相同数据限制的设备上的使用情况。 例如，在不同设备上使用同一 SIM 的系列计划。 移动宽带应用只应使用本地数据计数器来估算自上次同步到计费系统后的使用量。 对于已处理的数据使用，计费系统应视为权威系统。

### <a name="mobile-broadband-service"></a>移动宽带服务

移动宽带服务是一种 Windows 服务，它管理移动宽带 Api 与移动宽带设备之间的通信。 服务可以与任何其驱动程序符合 Windows Mobile 宽带驱动程序模型的移动宽带设备交互。

该服务还会读取新插入的设备的 SIM，并启动检索服务元数据的过程，以及与连接的移动宽带设备对应的移动宽带应用。

### <a name="mobile-broadband-class-driver"></a>移动宽带类驱动程序

移动宽带类驱动程序降低了设备制造商为其特定移动宽带设备提供自定义驱动程序的负担。 任何清单为 USB 设备并符合 USB 实现者论坛 (USB-如果) 网络控制模型 (NCM) 2.0 规范的移动宽带接口将由移动宽带类驱动程序管理，并且无需下载或安装其他驱动程序。

移动宽带类驱动程序符合 Windows Mobile 宽带驱动程序模型，并为移动宽带服务提供完整功能。 它还支持自定义扩展，这些扩展将直接公开到移动宽带应用。 有关详细信息，请参阅 [移动运营商硬件概述](mobile-operator-hardware-overview.md)。

### <a name="system-event-broker"></a>系统事件代理

系统事件代理管理后台事件。 应用（包括移动宽带应用）可以注册以接收后台事件以响应系统状态的更改。 移动宽带应用可能感兴趣的事件包括：

- **网络状态更改** -网络上的网络连接或断开连接或 Internet 连接已更改。

- **帐户状态更改** -计费周期结束或预计的数据使用增量为5%。

- **Wi-fi 热点身份验证** -需要尝试连接到公共 wi-fi 热点和凭据。

- **传入操作员通知** –与某些分析规则匹配的 SMS/USSD 消息，这些规则描述了从操作员那里描述的 SMS/USSD。

- **传入 sms** –接收到的 sms 消息与操作员定义的分析规则不匹配。

- 收到的**传入 USSD** – USSD 消息与运算符定义的分析规则不匹配。

开发人员应注意，严格的限制放置在应用程序处于非活动状态时可能使用的 CPU 时间量。 尽管这些限制对于某些事件是宽松的，但应用程序必须始终将其消耗的资源降至最低电量或其他应用程序运行时。

### <a name="windows-metadata-and-internet-services"></a>Windows 元数据和 Internet 服务

Windows 元数据和 Internet 服务 (WMIS) 是一项基于云的 Windows 服务，可从参与 Windows 设备生态系统的第三方向 Windows 提供自定义项。 对于移动宽带设备，WMIS 将提供服务元数据包。 这提供了 Windows 从 Microsoft Store 检索移动宽带应用程序所需的基本信息，允许首次连接到网络，并在 Windows 连接管理器中显示相应的品牌元素。

### <a name="microsoft-store"></a>Microsoft Store

Microsoft Store 是 UWP 应用传递到 Windows 8、Windows 8.1 和 Windows 10 电脑的主要方式。 对于移动宽带应用，只要在连接设备后可使用 Internet 连接，就会从 Microsoft Store 检索应用程序包。 此时会自动安装应用程序包，并将其提供给用户。 在 Windows 8.1 和 Windows 10 中，应用程序在 **所有应用** 程序中均可用，但不会自动固定到 "开始" 屏幕。

有关 UWP 设备应用的详细信息，请参阅 [uwp 设备应用](../devapps/index.md)。

**注意**   尽管企业可以在某些情况下加载 UWP 应用，但本文档不会介绍这些应用。

### <a name="operator-metadata"></a>运算符元数据

如下所述，在 Windows 8 和 Windows 10 中提供了三种不同方式的有关运算符的元数据。 每个元数据选项面向一组不同的客户。 了解如何传递三种类型的元数据，每种类型的信息将有助于您更好地满足客户的需要。

有关操作员元数据的详细信息，请参阅 [使用元数据配置移动宽带体验](using-metadata-to-configure-mobile-broadband-experiences.md)。

### <a name="windows-apn-database"></a>Windows APN 数据库

Windows APN 数据库存在于所有 Windows 8、Windows 8.1 和 Windows 10 电脑上。 数据库将通过使用 Windows 更新进行定期更新，以帮助确保连接信息的准确性。 数据库的更新通过您的服务请求进行。 APN 数据库向 Windows 提供有关如何连接到网络的信息（如果它遇到移动宽带设备），其中包括应尝试连接到的 APNs 以及用户在没有 Internet 连接的情况下应定向到的 URL。

此信息旨在让客户在连接移动宽带设备后的几秒钟内联机。 它应该允许他们通过使用 Web 浏览器立即购买服务，或在用户已购买服务时立即联机。

有关将更新提交到 Windows APN 数据库的信息，请参阅 [COSA/APN 数据库提交](cosa-apn-database-submission.md)。

### <a name="service-metadata"></a>服务元数据

服务元数据在连接移动宽带设备后会传递给任何用户。 始终会自动下载服务元数据，只要用户具有任何形式的 Internet 连接，包括按流量计费的移动宽带或漫游网络。

此信息使用户能够获得更丰富的体验，因为它允许你添加 Windows 连接管理器的品牌元素，引用自动从 Microsoft Store 获取的移动宽带应用，并具有最新的移动宽带设置以联机进行购买或 Internet 连接。 Windows 将定期检查它是否具有来自 WMIS 的最新服务元数据包。

仅当在电脑上检测到来自指定操作员的移动宽带设备时，才会将服务元数据包发送给客户。 此包中的信息会在存在时覆盖 APN 数据库的内容。 有关服务元数据包架构参考的详细信息，请参阅 [服务元数据包架构参考](service-metadata-package-schema-reference.md)。

有关如何创建服务元数据包的说明，请参阅 [创建服务元数据的开发人员指南](developer-guide-for-creating-service-metadata.md)。

### <a name="provisioning-metadata"></a>设置元数据

订阅者购买服务后，将通过操作员的网站或移动宽带应用将预配元数据传递到 PC。 预配元数据以 XML 文件的形式打包，并由预配代理处理以修改 PC 的网络设置。

可以为每个订阅服务器的单独要求指定预配元数据。 使用移动宽带应用，还可以使用更高的频率更新设置元数据。 设置元数据中的信息会替代 APN 数据库和服务元数据的内容。 这是因为它往往是最具体的有关订阅者的信息。