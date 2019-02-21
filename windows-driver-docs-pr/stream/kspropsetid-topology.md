---
title: KSPROPSETID\_拓扑
description: KSPROPSETID\_拓扑
ms.assetid: d0c51bcf-ced3-4863-9359-9fa326122262
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d802c243dc72e83b5f57efc37306eef529a751c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541276"
---
# <a name="kspropsetidtopology"></a>KSPROPSETID\_拓扑


## <span id="ddk_kspropsetid_topology_ks"></span><span id="DDK_KSPROPSETID_TOPOLOGY_KS"></span>


客户端使用请求中 KSPROPSETID\_拓扑属性设置为检查 KS 筛选器的内部拓扑。

在拓扑中的每个节点有一个从零开始的节点 ID:筛选 KS *n*节点将其编号从 0 到*n-1*。 整个 KS 筛选器本身可能会被视为一个节点，并且具有特殊的节点 ID 编号 KSFILTER\_节点。

Stream 微型驱动程序不需要处理中设置此属性的属性。 Stream 类驱动程序代表微型驱动程序处理它们。

Microsoft 定义了一组标准的节点类型的窗体 KSNODETYPE\_中的 XXX *ksmedia.h*标头文件。 当使用此集中的属性，客户端节点通过引用此序列中其从零开始的索引。

KSPROPSETID\_拓扑属性集包括：

[**KSPROPERTY\_拓扑\_类别**](ksproperty-topology-categories.md)

[**KSPROPERTY\_拓扑\_连接**](ksproperty-topology-connections.md)

[**KSPROPERTY\_拓扑\_名称**](ksproperty-topology-name.md)

[**KSPROPERTY\_拓扑\_节点**](ksproperty-topology-nodes.md)

 

 





