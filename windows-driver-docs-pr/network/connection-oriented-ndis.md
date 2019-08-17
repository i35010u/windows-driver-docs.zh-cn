---
title: 面向连接的 NDIS 简介
description: 面向连接的 NDIS 简介
ms.assetid: c74f8e60-c041-48e9-8aa1-98a9cb9eb869
keywords:
- 面向连接的 NDIS WDK
- CoNDIS WDK 网络
- 网络驱动程序 WDK, CoNDIS
- NDIS WDK, CoNDIS
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 292d23d394ba300caa4d1f7a413b228fb973d23b
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565770"
---
# <a name="connection-oriented-ndis"></a>面向连接的 NDIS

本部分介绍面向连接的 NDIS (CoNDIS)。 大多数 CoNDIS 6.0 和更高版本的驱动程序操作未从其 CoNDIS 5 发生更改。*x*版本。 有关 CoNDIS 1.x 和 CoNDIS 6.0 之间的差异的详细信息, 请参阅[将 CoNDIS 驱动程序迁移到 CoNDIS 6.0](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-a-condis-5-x-driver-to-condis-6-0)。

除非另有说明, 否则 CoNDIS 驱动程序提供的服务与无连接 NDIS 驱动程序相同。 在尝试编写 CoNDIS 驱动程序之前, 应熟悉无连接 NDIS 驱动程序。 有关无连接 NDIS 驱动程序的详细信息, 请参阅[编写 Ndis 微型端口驱动程序](writing-ndis-miniport-drivers.md)、[编写 ndis 协议驱动](writing-ndis-protocol-drivers.md)程序和[编写 ndis 中间驱动程序](writing-ndis-intermediate-drivers.md)。

以下各节介绍面向连接的 NDIS:

[面向连接的环境](connection-oriented-environment.md)

[使用 AFs、VCs、Sap 和参与方](using-afs--vcs--saps--and-parties.md)

[服务质量](quality-of-service.md)

[MCM 驱动程序与呼叫管理器](mcm-drivers-vs--call-managers.md)

[面向连接的计时功能](connection-oriented-timing-features.md)

[CoNDIS 注册](condis-registration.md)

[面向连接的操作](connection-oriented-operations.md)

 

 





