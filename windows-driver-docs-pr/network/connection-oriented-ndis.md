---
title: 面向连接的 NDIS
description: 面向连接的 NDIS
ms.assetid: c74f8e60-c041-48e9-8aa1-98a9cb9eb869
keywords:
- 面向连接的 NDIS WDK
- 网络的 CoNDIS WDK
- 网络驱动程序 WDK，CoNDIS
- NDIS WDK CoNDIS
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0a1292d411c851a0e5f66cc23ba1bfa2093d04e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562273"
---
# <a name="connection-oriented-ndis"></a>面向连接的 NDIS





本部分介绍面向连接的 NDIS (CoNDIS)。 从其的 CoNDIS 5 未更改大多数的 CoNDIS 6.0 和更高版本的驱动程序操作。*x*版本。 有关详细信息的 CoNDIS 之间的差异 5.x 和 CoNDIS 6.0，请参阅[移植的 CoNDIS 5.x 驱动程序的 CoNDIS 6.0](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-a-condis-5-x-driver-to-condis-6-0)。

除非另有说明，CoNDIS 驱动程序提供与无连接的 NDIS 驱动程序相同的服务。 在尝试编写的 CoNDIS 驱动程序之前，您应熟悉无连接的 NDIS 驱动程序。 有关无连接的 NDIS 驱动程序的详细信息，请参阅[编写 NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)，[编写 NDIS 协议驱动程序](writing-ndis-protocol-drivers.md)，和[编写 NDIS 中间驱动程序](writing-ndis-intermediate-drivers.md).

以下部分介绍了面向连接的 NDIS:

[面向连接的环境](connection-oriented-environment.md)

[使用 AFs、 VCs、 SAPs 和参与方](using-afs--vcs--saps--and-parties.md)

[服务质量](quality-of-service.md)

[MCM 驱动程序 vs。调用管理器](mcm-drivers-vs--call-managers.md)

[面向连接的计时功能](connection-oriented-timing-features.md)

[CoNDIS 注册](condis-registration.md)

[面向连接的操作](connection-oriented-operations.md)

 

 





