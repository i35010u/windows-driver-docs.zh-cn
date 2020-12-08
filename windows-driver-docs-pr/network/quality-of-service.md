---
title: 服务质量
description: 服务质量
keywords:
- 面向连接的 NDIS WDK，服务质量
- CoNDIS WDK 网络，服务质量
- 服务质量 WDK CoNDIS
- QoS WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84d95d35fdfbe789364d0e19a3a140dfdb0af97f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791381"
---
# <a name="quality-of-service"></a>服务质量





在 SVC 上调用的发起方可以指定 *服务* (QoS) 参数，以指定调用的性能参数。 根据正在使用的信号协议，设置传出或传入呼叫的呼叫管理器或 MCM 驱动程序可以使用网络实体（例如网络交换机或远程客户端）来协商 QoS。 如果信号协议允许，则面向连接的客户端在确定是否接受传入呼叫时，还可能会请求更改 QoS。

调用的 QoS 参数指定为 [**CO \_ 调用 \_ 参数**](/previous-versions/windows/hardware/network/ff545384(v=vs.85)) 结构中的调用参数。 CO \_ 调用 \_ 参数指向两个其他结构：

-   [**共同 \_调用 \_ 管理器 \_ 参数**](/previous-versions/windows/hardware/network/ff545381(v=vs.85))，指定调用管理器或 MCM 驱动程序用于设置呼叫的调用管理器参数。

-   [**共同 \_媒体 \_ 参数**](/previous-versions/windows/hardware/network/ff545388(v=vs.85))，指定微型端口驱动程序或 MCM 驱动程序用于激活 VC 的媒体参数。

共同 \_ 调用 \_ 管理器 \_ 参数和 co \_ 媒体 \_ 参数都包含适用于使用参数的所有驱动程序 (标志) 的泛型参数。 其中的每个结构还指向 [**co \_ 特定的 \_ 参数**](/previous-versions/windows/hardware/network/ff545396(v=vs.85)) 结构，该结构指定由 co \_ 调用 \_ 管理器 \_ 参数结构指向) 或特定于媒体参数的参数， (当 co \_ media \_ parameters 结构) 时， (指定调用管理器特定的参数。

有关 QoS 操作的详细信息，请参阅 [客户端启动的更改调用参数的请求](client-initiated-request-to-change-call-parameters.md) 和 [用于更改调用参数的传入请求](incoming-request-to-change-call-parameters.md)。

 

