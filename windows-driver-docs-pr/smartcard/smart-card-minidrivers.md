---
title: 智能卡微型驱动器
description: 智能卡微型驱动器
ms.assetid: BE24E8C3-663A-47A3-B30C-CBB0AEF89E45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38cd1142d830315a4bf55e64b6e1624e1de32399
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382697"
---
# <a name="smart-card-minidrivers"></a>智能卡微型驱动器


智能卡微型驱动程序提供了一种更简单的替代方法，用于通过封装来自智能卡微型驱动程序开发人员的大多数复杂加密操作来开发旧式加密服务提供程序 (CSP)。

有关智能卡微型驱动程序规范的信息，请参阅 [智能卡微型驱动程序规范](/previous-versions/windows/hardware/design/dn631754(v=vs.85))。

从 Windows Vista 开始，应用程序可以使用 Microsoft 加密 API：下一代 (CNG) 用于基于智能卡的加密服务。 作为椭圆曲线加密的一部分， (Windows Vista 中引入的 ECC) 工作量，新的加密框架支持 ECC 智能卡。 与现有的 Rivest-Rivest-shamir-adleman-Rivest-shamir-adleman (RSA) 卡微型驱动程序通过旧的 CAPI 子系统进行交互的应用程序和接口在未修改的情况下继续运行。

RSA 智能卡微型驱动程序也可以注册到智能卡密钥存储提供程序 (KSP) ，以便可以通过 CNG 接口调用。 双模式 ECC/RSA + 仅 ECC 的请求会路由到 KSP，并通过它发送到相应的卡微型驱动程序。 对于基于 Windows Vista 的客户端，使用 Windows 智能卡框架支持仅限 ECC 和 ECC/RSA 双模式卡。 还可以通过 CAPI 访问双模式卡，主要用于公开仅限 RSA 的功能。

应用程序将 CAPI 用于基于智能卡的加密服务。 CAPI 进而会将这些请求路由到相应的 CSP 来处理加密要求。

Microsoft 智能卡基本 CSP 和 KSP 是体系结构的一项改进，它们分别与必须为每个卡供应商更改的实现详细信息分开。

尽管基本 CSP 只能通过使用微型驱动程序来使用智能卡的 RSA 功能，但基于 CNG 的 KSP 仅支持 Windows Vista 和更高版本的 Windows 中的 ecc/RSA 双模式智能卡。

最终，这一目的是为了支持新的体系结构，以支持所有新智能卡-RSA、ECC，还包括以下任何内容。 它将 CSP 的实现拆分为两个部分：

-   基本 CSP/KSP (常见部分) ，其中包括哈希、对称和公钥加密操作的功能以及个人标识号 (PIN) 条目和缓存。
-   一系列插件（称为 "卡微型驱动程序"），可将特定智能卡的特征转换为适用于所有智能卡的统一接口。 然后，卡微型驱动程序使用智能卡资源管理器的服务与卡通信 (SCRM) ，这同样会对各种智能卡读卡器的特征进行抽象化。

智能卡供应商的其余部分是实现卡微型驱动程序，这是一个合理的有限接口层，它提供了卡到基本 CSP/KSP 的抽象，并按文件系统和一组基元功能进行组织。 高阶功能（如缓存 (确保卡上的不同文件) 或处理命名冲突，在较高的级别（在卡微型驱动程序外）进行处理。

下图显示了卡微型驱动程序和基于 CAPI 的应用程序之间的接口。

![卡微型驱动程序和基于 capi 的应用程序之间的接口](images/capiinterface.png)

下图显示了卡微型驱动程序与基于 CAPI2 的应用程序之间的接口。

![卡微型驱动程序和基于 capi2 的应用程序之间的接口](images/capi2interface.png)

建议开发人员充分利用 Microsoft 为微型驱动程序执行的加密操作提供的一组丰富的库。 这样，开发人员便可以受益于 Microsoft Windows 更新基础结构，以便分发重要的安全更新。

 

