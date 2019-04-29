---
title: CoNDIS WAN 驱动程序的 WAN 特定功能
description: CoNDIS WAN 驱动程序的 WAN 特定功能
ms.assetid: c4e8e0ae-7dd5-4c4e-900a-b1f7e5eecb16
keywords:
- CoNDIS WAN 的驱动程序 WDK 网络，与非 WAN CoNDIS 驱动程序
- 非 WAN CoNDIS 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa3de90c84344d699449cf7a8689001c260e9e7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380568"
---
# <a name="wan-specific-capabilities-of-condis-wan-drivers"></a>CoNDIS WAN 驱动程序的 WAN 特定功能





WAN 的 CoNDIS 驱动程序不同于非 WAN CoNDIS 驱动程序，如下所示：

-   WAN 的 CoNDIS 支持驱动程序的 TAPI 服务使用产生的 CO\_地址\_系列\_TAPI\_代理地址族。

-   WAN 的 CoNDIS 驱动程序支持特定于 WAN 的 Oid:[OID\_WAN\_永久\_地址](https://msdn.microsoft.com/library/windows/hardware/ff561220)， [OID\_WAN\_当前\_地址](https://msdn.microsoft.com/library/windows/hardware/ff561200)，并[OID\_WAN\_中等\_子类型](https://msdn.microsoft.com/library/windows/hardware/ff561216)。

-   WAN 的 CoNDIS 微型端口驱动程序支持 CoNDIS WAN Oid 到集和查询操作特征的集。 有关的 CoNDIS WAN Oid 的详细信息，请参阅[CoNDIS WAN 对象](https://msdn.microsoft.com/library/windows/hardware/ff545146)。

-   TAPI 服务提供的 CoNDIS WAN 微型端口驱动程序支持 CoNDIS TAPI Oid 到集和查询操作特征的集。 有关的 CoNDIS TAPI Oid 的详细信息，请参阅[Connection-Oriented ndis TAPI 扩展](https://msdn.microsoft.com/library/windows/hardware/ff570924)。

-   WAN 的 CoNDIS 微型端口驱动程序支持一系列表示链接的状态更改的特定于 WAN 的状态指示。 有关的 CoNDIS WAN 微型端口驱动程序状态指示的详细信息，请参阅[，该值指示的 CoNDIS WAN 微型端口驱动程序状态](indicating-condis-wan-miniport-driver-status.md)。

-   WAN 的 CoNDIS 微型端口驱动程序保持一组特定于 WAN 的统计信息。 [OID\_WAN\_共同\_获取\_统计信息\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569820)OID 请求要返回的统计信息的微型端口驱动程序。

-   永远不会尝试返回循环; 的任何数据包的 CoNDIS WAN 微型端口驱动程序NDISWAN 提供环回支持。

 

 





