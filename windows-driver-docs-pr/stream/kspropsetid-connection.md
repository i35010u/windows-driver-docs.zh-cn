---
title: KSPROPSETID \_ 连接
description: KSPROPSETID \_ 连接
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7578b49dd2a6f5bde01e0e3ecfa689552d5aeeb2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828339"
---
# <a name="kspropsetid_connection"></a>KSPROPSETID \_ 连接


## <span id="ddk_kspropsetid_connection_ks"></span><span id="DDK_KSPROPSETID_CONNECTION_KS"></span>


客户端使用 KSPROPSETID \_ 连接属性中设置的属性来检查或设置 pin 的连接状态。 固定实例将处理这些属性。

Stream 类微型驱动程序不必直接处理 [**KSPROPERTY \_ 连接 \_ 状态**](ksproperty-connection-state.md) 或 [**KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md) 属性。 流类驱动程序处理它们，使用流请求块 (SRB) 在必要时查询详细信息。

KSPROPSETID \_ 连接属性集包括：

[**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

[**KSPROPERTY \_ 连接 \_ ALLOCATORFRAMING \_ EX**](ksproperty-connection-allocatorframing-ex.md)

[**KSPROPERTY \_ 连接 \_ ACQUIREORDERING**](ksproperty-connection-acquireordering.md)

[**KSPROPERTY \_ 连接 \_ DATAFORMAT**](ksproperty-connection-dataformat.md)

[**KSPROPERTY \_ 连接 \_ 优先级**](ksproperty-connection-priority.md)

[**KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSPROPERTY \_ 连接 \_ STARTAT**](ksproperty-connection-startat.md)

[**KSPROPERTY \_ 连接 \_ 状态**](ksproperty-connection-state.md)

 

 





