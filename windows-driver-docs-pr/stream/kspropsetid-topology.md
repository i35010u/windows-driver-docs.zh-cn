---
title: KSPROPSETID \_ 拓扑
description: KSPROPSETID \_ 拓扑
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aff27e4d2f82235b9a73e00ce9a59886aab77e42
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814859"
---
# <a name="kspropsetid_topology"></a>KSPROPSETID \_ 拓扑


## <span id="ddk_kspropsetid_topology_ks"></span><span id="DDK_KSPROPSETID_TOPOLOGY_KS"></span>


客户端使用 KSPROPSETID \_ 拓扑属性集中的请求来检查 KS 筛选器的内部拓扑。

拓扑中的每个节点都有一个从零开始的节点 ID：包含 *n* 个节点的 KS 筛选器将其从0到 *n-1* 进行编号。 整个 KS 筛选器本身可能被视为一个节点，并且具有特殊节点 ID 号 KSFILTER \_ 节点。

Stream 微型驱动程序无需处理此属性集中的属性。 流类驱动程序代表微型驱动程序处理它们。

Microsoft 在 \_ *ksmedia* 标头文件中定义了一组标准的 KSNODETYPE XXX 形式的节点类型。 使用此集中的属性时，客户端通过此序列中的从零开始的索引引用节点。

KSPROPSETID \_ 拓扑属性集包括：

[**KSPROPERTY \_ 拓扑 \_ 类别**](ksproperty-topology-categories.md)

[**KSPROPERTY \_ 拓扑 \_ 连接**](ksproperty-topology-connections.md)

[**KSPROPERTY \_ 拓扑 \_ 名称**](ksproperty-topology-name.md)

[**KSPROPERTY \_ 拓扑 \_ 节点**](ksproperty-topology-nodes.md)

 

 





