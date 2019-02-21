---
title: KSPROPSETID\_连接
description: KSPROPSETID\_连接
ms.assetid: 1be062ab-7396-4876-ab28-8a03e55df1d3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64d73eff27563ce37aad3448f888b8530b765857
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521247"
---
# <a name="kspropsetidconnection"></a>KSPROPSETID\_连接


## <span id="ddk_kspropsetid_connection_ks"></span><span id="DDK_KSPROPSETID_CONNECTION_KS"></span>


客户端使用属性中 KSPROPSETID\_连接属性设置为检查或 pin 设置连接的状态。 Pin 实例处理这些属性。

Stream 类微型驱动程序无需处理[ **KSPROPERTY\_连接\_状态**](ksproperty-connection-state.md)或者[ **KSPROPERTY\_连接\_PROPOSEDATAFORMAT** ](ksproperty-connection-proposedataformat.md)直接属性。 Stream 类驱动程序处理它们，使用流请求块 (SRB) 查询的详细信息，如有必要。

KSPROPSETID\_连接属性集包括：

[**KSPROPERTY\_连接\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

[**KSPROPERTY\_CONNECTION\_ALLOCATORFRAMING\_EX**](ksproperty-connection-allocatorframing-ex.md)

[**KSPROPERTY\_连接\_ACQUIREORDERING**](ksproperty-connection-acquireordering.md)

[**KSPROPERTY\_连接\_DATAFORMAT**](ksproperty-connection-dataformat.md)

[**KSPROPERTY\_连接\_优先级**](ksproperty-connection-priority.md)

[**KSPROPERTY\_CONNECTION\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSPROPERTY\_连接\_STARTAT**](ksproperty-connection-startat.md)

[**KSPROPERTY\_连接\_状态**](ksproperty-connection-state.md)

 

 





