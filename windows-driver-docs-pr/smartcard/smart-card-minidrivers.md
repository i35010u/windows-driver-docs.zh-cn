---
title: 智能卡微型驱动器
description: 智能卡微型驱动器
ms.assetid: BE24E8C3-663A-47A3-B30C-CBB0AEF89E45
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb20231b804bdb47e4228c078562c730e7220aaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382559"
---
# <a name="smart-card-minidrivers"></a>智能卡微型驱动器


智能卡微型驱动程序通过封装的大多数复杂的加密操作卡微型驱动程序开发人员提供更简单的替代开发旧的加密服务提供程序 (CSP)。

有关智能卡微型驱动程序的规范的信息，请参阅[智能卡微型驱动程序规范](https://msdn.microsoft.com/library/windows/hardware/dn631754)。

从 Windows Vista 开始，应用程序可以使用 Microsoft 加密 API:下一代 (CNG) 的基于智能卡加密服务。 在 Windows Vista 中引入的椭圆曲线加密 (ECC) 工作的一部分，在新的加密框架支持 ECC 智能卡。 应用程序和与现有 Rivest 仅使用 Adleman (RSA) 卡微型驱动程序通过旧 CAPI 子系统进行交互的接口继续无需修改即可。

以便可以通过 CNG 接口调用它们，也可以使用智能卡密钥存储提供程序 (KSP) 注册 RSA 智能卡微型驱动程序。 双模式 ECC/RSA + 仅限 ECC 的请求路由到 KSP，以及通过它，到适当的卡微型驱动程序。 对于基于 Windows Vista 客户端，通过使用 Windows 智能卡框架支持仅使用 ECC 和 ECC/RSA 双模式卡。 此外可以通过 CAPI 主要用于公开 RSA 功能访问双模式卡。

应用程序使用 CAPI 的基于智能卡加密服务。 CAPI，反过来，将这些请求路由到相应的 CSP 来处理加密的要求。

Microsoft Smart Card Base CSP 和 KSP 是通常用于分隔的体系结构的优化需要基于 CAPI 的 CSP 和 KSP 基于 CNG 的功能，分别为每个卡供应商必须更改的实现细节。

尽管基本 CSP 可以使用智能卡的 RSA 功能只能通过使用微型驱动程序，但基于 CNG 的 KSP 在 Windows Vista 和更高版本的 Windows 支持 ECC 限以及 ECC/RSA 双模式智能卡。

从根本上讲，目的是为新的体系结构来支持所有新的智能卡 — RSA、 ECC，和任何如下所示。 它将拆分为两个部分的 CSP 的实现：

-   基本 CSP/KSP （常见的一部分），其中包括功能进行哈希处理，对称和公钥加密操作除了个人标识号 (pin) 条目和缓存。
-   一系列的插件，名为"卡微型驱动程序，"的转换是相同的所有智能卡的统一接口为特定智能卡的特征。 卡微型驱动程序然后与他们的卡通信，通过使用同样抽象化各种智能卡读卡器的特征的智能卡资源管理器 (SCRM) 服务。

智能卡供应商的剩余部分是卡的实现卡微型驱动程序，以合理方式有限的接口层，它提供抽象到基本 CSP/KSP 和组织文件系统，和一组基元的功能。 在较高级别，外部卡微型驱动程序处理更高的顺序功能，如缓存 （确保在卡上的不同文件具有一致的内容） 或处理命名冲突。

下图显示了卡微型驱动程序和基于 CAPI 的应用程序之间的接口。

![卡微型驱动程序和基于 capi 的应用程序之间的接口](images/capiinterface.png)

下图显示了卡微型驱动程序和基于 CAPI2 的应用程序之间的接口。

![卡微型驱动程序和基于 capi2 的应用程序之间的接口](images/capi2interface.png)

它是建议开发人员充分利用一组丰富的库，Microsoft 提供的微型驱动程序执行加密操作。 这使开发人员受益的关键安全更新的分发的 Microsoft Windows 更新基础结构。

 

 





