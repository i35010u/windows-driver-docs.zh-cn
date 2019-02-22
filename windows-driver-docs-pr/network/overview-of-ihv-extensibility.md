---
title: IHV 扩展性概述
description: IHV 扩展性概述
ms.assetid: 446d91e9-3497-4b45-82a6-7f36dd136e08
keywords:
- IHV 扩展 WDK 本机 802.11 有关 IHV 扩展性
- 本机 802.11 IHV 扩展 WDK，有关 IHV 扩展性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65de079b2e210c23b399a77930808326041629c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526907"
---
# <a name="overview-of-ihv-extensibility"></a>IHV 扩展性概述




 

本机 802.11 框架提供了对将功能添加到本机 802.11 框架的独立硬件供应商 (IHV) 的支持。

例如，IHV 可以为以下任一提供支持：

-   基于端口的网络访问的专有或非标准身份验证算法。 有关详细信息，请参阅[802.11 身份验证算法的扩展支持](extending-support-for-802-11-authentication-algorithms.md)。

-   数据加密的专有或非标准密码算法。 有关详细信息，请参阅[802.11 密码算法的扩展支持](extending-support-for-802-11-cipher-algorithms.md)。

-   专用物理配置。 有关详细信息，请参阅[802.11 的物理配置的扩展支持](extending-support-for-802-11-phy-configurations.md)。

若要扩展的本机 802.11 功能，IHV 必须提供以下组件：

-   本机 802.11 微型端口驱动程序支持的可扩展工作站 (ExtSTA) 操作模式。 有关此模式的详细信息，请参阅[可扩展工作站操作模式下](extensible-station-operation-mode.md)。 详细了解方式 ExtSTA 操作模式如何扩展本机 802.11 的功能，请参阅[扩展本机 802.11 功能](extending-native-802-11-functionality.md)。

-   IHV 扩展 DLL，它会处理 IHV 支持的专有身份验证算法通过交换的安全数据包。 IHV 扩展 DLL 也是负责通过这些身份验证算法，以及与支持 IHV 的安全扩展插件相关的用户数据的验证的加密密钥派生的。

    IHV 扩展 DLL 的详细信息，请参阅[本机 802.11 IHV 扩展 DLL](native-802-11-ihv-extensions-dll4.md)。

-   IHV 用户界面 (UI) 扩展 DLL，该类用于扩展本机 802.11 用户界面来配置连接和安全设置，验证和处理的 IHV 扩展 DLL。

    IHV UI 扩展 DLL 的详细信息，请参阅[本机 802.11 IHV UI 扩展 DLL](native-802-11-ihv-ui-extensions-dll2.md)。

有关由 IHV 提供的模块的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

若要提供一个安全的执行环境，IHV 应执行以下操作：

1.  不要在事件中记录任何敏感信息，如加密密钥，或调试日志。

2.  使用[CryptProtectMemory](https://go.microsoft.com/fwlink/p/?linkid=64677)来保护敏感的加密密钥存储在内存中，并[SecureZeroMemory](https://go.microsoft.com/fwlink/p/?linkid=64678)清除内存时使用密钥来完成。

3.  将处理的 IHV 扩展部分[网络配置文件](configuration-through-a-network-profile.md)作为不受信任的数据被攻击者所操控。 IHV 扩展部分的配置文件是不透明的 802.11 自动配置模块 (ACM) 和媒体特定模块 (MSM)，并将不会验证。 (请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)有关这些模块和配置控件路径的说明。)应适当地分析此 IHV 扩展数据以防止任何缓冲区溢出或可能会导致权限本地特权提升攻击。

 

 





