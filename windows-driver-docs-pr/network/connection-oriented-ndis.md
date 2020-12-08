---
title: “面向连接的 NDIS”简介
description: “面向连接的 NDIS”简介
keywords:
- 面向连接的 NDIS WDK
- CoNDIS WDK 网络
- 网络驱动程序 WDK，CoNDIS
- NDIS WDK，CoNDIS
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: db163cb9c6ed06a58818ed89c34f8defc5757b58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783843"
---
# <a name="connection-oriented-ndis"></a>面向连接的 NDIS

本部分介绍面向连接的 NDIS (CoNDIS) 。 大多数 CoNDIS 6.0 和更高版本的驱动程序操作未从其 CoNDIS 5 发生更改。*x* 版本。 有关 CoNDIS 1.x 和 CoNDIS 6.0 之间的差异的详细信息，请参阅 [将 CoNDIS 驱动程序迁移到 CoNDIS 6.0](/previous-versions/windows/hardware/network/porting-a-condis-5-x-driver-to-condis-6-0)。

除非另有说明，否则 CoNDIS 驱动程序提供的服务与无连接 NDIS 驱动程序相同。 在尝试编写 CoNDIS 驱动程序之前，应熟悉无连接 NDIS 驱动程序。 有关无连接 NDIS 驱动程序的详细信息，请参阅 [编写 Ndis 微型端口驱动程序](./initializing-a-miniport-driver.md)、 [编写 ndis 协议驱动](initializing-a-protocol-driver.md)程序和 [编写 ndis 中间驱动程序](writing-ndis-intermediate-drivers.md)。

以下各节介绍面向连接的 NDIS：

[面向连接的环境](connection-oriented-environment.md)

[使用 AF、VC、SAP 和参与方](using-afs--vcs--saps--and-parties.md)

[服务质量](quality-of-service.md)

[MCM 驱动程序与呼叫管理程序](mcm-drivers-vs--call-managers.md)

[面向连接的计时功能](connection-oriented-timing-features.md)

[CoNDIS 注册](condis-miniport-driver-registration.md)

[面向连接的操作](connection-oriented-operations-performed-by-clients.md)

 

