---
title: IHV 可扩展性概述
description: IHV 可扩展性概述
ms.assetid: 446d91e9-3497-4b45-82a6-7f36dd136e08
keywords:
- IHV 扩展 WDK 本机802.11，关于 IHV 扩展性
- 本机 802.11 IHV 扩展 WDK，关于 IHV 扩展性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b7c22323c687d0148dc9533471431a978a319aa
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208599"
---
# <a name="overview-of-ihv-extensibility"></a>IHV 可扩展性概述




 

本机802.11 框架为独立硬件供应商 (IHV 提供支持) 将功能添加到本机 802.11 framework。

例如，IHV 可以为以下任何内容提供支持：

-   用于基于端口的网络访问的专有或非标准身份验证算法。 有关详细信息，请参阅 [扩展对802.11 身份验证算法的支持](/previous-versions/windows/hardware/wireless/extending-support-for-802-11-authentication-algorithms)。

-   用于数据加密的专有或非标准密码算法。 有关详细信息，请参阅 [扩展对802.11 密码算法的支持](/previous-versions/windows/hardware/wireless/extending-support-for-802-11-cipher-algorithms)。

-   专有 PHY 配置。 有关详细信息，请参阅 [扩展对 802.11 PHY 配置的支持](/previous-versions/windows/hardware/wireless/extending-support-for-802-11-phy-configurations)。

为了扩展本机802.11 功能，IHV 必须提供以下组件：

-   支持可扩展工作站 (ExtSTA) 操作模式的本机802.11 微型端口驱动程序。 有关此模式的详细信息，请参阅 [可扩展工作站操作模式](/previous-versions/windows/hardware/wireless/extensible-station-operation-mode)。 有关 ExtSTA 操作模式可以扩展本机802.11 功能的方式的详细信息，请参阅 [扩展本机802.11 功能](/previous-versions/windows/hardware/wireless/extending-native-802-11-functionality)。

-   一个 IHV 扩展 DLL，它处理通过 IHV 支持的专有身份验证算法交换的安全数据包。 IHV 扩展 DLL 还负责通过这些身份验证算法进行密码密钥派生，并负责验证与 IHV 支持的安全扩展有关的用户数据。

    有关 IHV 扩展 DLL 的详细信息，请参阅 [Native 802.11 IHV EXTENSION dll](native-802-11-ihv-extensions-dll4.md)。

-   一个 IHV 用户界面 (UI) 扩展 DLL，该 DLL 扩展了本机802.11 用户界面，以配置由 IHV 扩展 DLL 验证和处理的连接和安全设置。

    有关 IHV UI 扩展 DLL 的详细信息，请参阅 [本机 802.11 IHV Ui 扩展 dll](native-802-11-ihv-ui-extensions-dll2.md)。

有关 IHV 提供的模块的详细信息，请参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture)。

为了提供安全的执行环境，IHV 应执行以下操作：

1.  不要将任何敏感信息（如加密密钥）记录在事件日志或调试日志中。

2.  使用 [CryptProtectMemory](https://go.microsoft.com/fwlink/p/?linkid=64677) 来保护存储在内存中的敏感加密密钥，并使用 [SecureZeroMemory](https://go.microsoft.com/fwlink/p/?linkid=64678) 在密钥完成时清除内存。

3.  将 [网络配置文件](/previous-versions/windows/hardware/wireless/configuration-through-a-network-profile) 的 IHV 扩展部分视为可能由攻击者操作的不受信任的数据。 配置文件的 IHV 扩展部分对于802.11 自动配置模块是不透明的， () 和媒体特定模块 (MSM) ，并且将不会进行验证。  (参阅 [本机802.11 软件体系结构](/previous-versions/windows/hardware/wireless/native-802-11-software-architecture) ，了解有关这些模块和配置控制路径的说明 ) 。应适当地分析此 IHV 扩展数据，以防止任何缓冲区溢出或可能导致本地升级权限的攻击。

 

 