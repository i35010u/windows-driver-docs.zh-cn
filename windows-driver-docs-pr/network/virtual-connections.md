---
title: 虚拟连接
description: 虚拟连接
ms.assetid: becb3acf-2a23-408a-8d1f-ff8a1e7ffe61
keywords:
- 面向连接的 NDIS WDK，虚拟连接
- CoNDIS WDK 网络、 虚拟连接
- 虚拟连接 WDK 的 CoNDIS
- 有关虚拟连接的虚拟连接 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6820b06a00bcfb7211dd1de311f6427d0fe79967
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565106"
---
# <a name="virtual-connections"></a>虚拟连接





在本地计算机上 *(VC) 的虚拟连接*为终结点 （或关联），可以托管客户端、 呼叫管理器或 MCM 驱动程序和微型端口驱动程序之间的单一调用。 在网络上，VC 是指两个通信的终结点，例如，两个面向连接的客户端之间的连接。

许多 VCs 可以处于活动状态 NIC 上一次启用要同时服务许多调用的 NIC。 每个连接可以是到不同的计算机上的不同终结点。

在网络上的 VCs 改变它们向客户端提供的服务的类型。 例如，VC 可以提供单向或双向服务。 服务质量 (QoS) 参数的每个方向可以保证特定性能阈值，如带宽和延迟。 根据信号协议，VC QoS 可能协商。 有关 NDIS 支持 QoS 的详细信息，请参阅[的服务质量](quality-of-service.md)。

在网络上的 VC 可以交换 VC (SVC) 或永久 VC (PVC):

-   SVC 创建所需的特定调用。 例如，面向连接的客户端启动的传出调用，它会使 VC 的创建。 同样，呼叫管理器或 MCM 驱动程序启动它会指示面向连接的客户端的传入呼叫的 VC 的创建。 呼叫管理器或 MCM 驱动程序必须进行通信，并有时协商与远程方 VC 参数。

-   永久 VC 手动创建，并最终删除通过使用配置实用程序，它不提供在 NDIS 运算符。 可以使用客户端，用于监视此类手动创建和删除的 Pvc [OID\_共同\_添加\_PVC](https://msdn.microsoft.com/library/windows/hardware/ff569087)并[OID\_共同\_删除\_PVC](https://msdn.microsoft.com/library/windows/hardware/ff569090) Oid 请求呼叫管理器或 MCM 驱动程序添加或删除 PVC 到或从其已配置 Pvc 的列表。 有关 PVC QoS 由操作员配置，并通过网络不协商。

在 NDIS，VC 包括由维护有关 VC 网络上的状态信息的微型端口驱动程序分配的资源。 这些资源可能包括但不限于内存缓冲区、 事件和数据结构。 微型端口驱动程序请求的传入呼叫管理器为 VC 面向连接的客户端的传出调用或调用创建此类上下文。 有关创建 VCs 的详细信息，请参阅[创建 VC](creating-a-vc.md)。

创建的 VC 可用于数据传输之前，必须通过呼叫管理器或 MCM 驱动程序来激活它。 若要激活 VC，微型端口驱动程序或 MCM 驱动程序设置 VC 资源并根据需要来准备要接收或传输 VC 上的数据的 NIC 的 NIC 与进行通信。 VC 激活有关的详细信息，请参阅[激活 VC](activating-a-vc.md)。

当关闭调用、 呼叫管理器或 MCM 驱动程序[停用 VC](deactivating-a-vc.md)用于调用。

VC （面向连接的客户端、 呼叫管理器或 MCM 驱动程序） 的创建者调用，则将调用后，可以使用任一启动[VC 删除](deleting-a-vc.md)或 VC 用于另一个调用。

 

 





