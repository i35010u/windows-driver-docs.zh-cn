---
title: 服务质量
description: 服务质量
ms.assetid: e7a4413c-633b-4634-a647-c84b8c97cbea
keywords:
- 面向连接的 NDIS WDK、 服务质量
- 网络服务质量的 CoNDIS WDK
- WDK 的 CoNDIS 服务质量
- QoS WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba250c892ae3cdecc4f5918adf294fc3ae116720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576235"
---
# <a name="quality-of-service"></a>服务质量





可以指定对 SVC 调用发起方*服务的质量*调用指定该调用的性能参数 (QoS) 参数。 根据信号协议，它是正在使用、 呼叫管理器或设置一个传出或传入调用的 MCM 驱动程序可以协商网络实体，例如网络交换机或远程客户端与 QoS。 如果允许信号协议，面向连接的客户端还可能会请求的 QoS 的更改，确定是否接受的传入呼叫时。

调用的 QoS 参数指定作为调用的参数[**共同\_调用\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545384)结构。 CO\_调用\_参数指向两个其他结构：

-   [**CO\_调用\_MANAGER\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545381)，用于指定调用管理器参数呼叫管理器或用于设置调用的 MCM 驱动程序。

-   [**CO\_媒体\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545388)，它指定媒体参数的微型端口驱动程序或使用激活 VC MCM 驱动程序。

这两个共同\_调用\_MANAGER\_参数和 CO\_媒体\_参数包含将应用于所有驱动程序的使用的参数的泛型参数 （标志）。 每个这些结构还指向[**共同\_特定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545396)结构，它指定调用特定于管理器的参数 (时指向共同\_调用\_MANAGER\_参数结构) 或特定于媒体的参数 (时指向共同\_媒体\_参数结构)。

有关 QoS 的操作的详细信息，请参阅[Client-Initiated 请求更改调用参数](client-initiated-request-to-change-call-parameters.md)并[对更改调用参数的传入请求](incoming-request-to-change-call-parameters.md)。

 

 





