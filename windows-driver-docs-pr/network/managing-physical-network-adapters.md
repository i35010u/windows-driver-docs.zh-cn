---
title: 管理物理网络适配器
description: 管理物理网络适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 756dfd66fd42bcf10ebf3763617bad07d09f383d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820085"
---
# <a name="managing-physical-network-adapters"></a>管理物理网络适配器


本部分介绍 Hyper-v 可扩展交换机扩展可对绑定到可扩展交换机外部网络适配器的底层物理适配器执行的操作。

这些操作允许扩展将对象标识符转发或发起 (OID) 请求到基础物理网络适配器。 扩展还可以在可扩展交换机驱动程序堆栈上从物理网络适配器转发或产生 NDIS 状态指示。

**注意**  此类操作的操作只能由可扩展的切换转发扩展执行。 有关此类型的扩展的详细信息，请参阅 [转发扩展](forwarding-extensions.md)。

 

本节包括下列主题：

[管理物理网络适配器连接状态](forwarding-packets-to-physical-network-adapters.md)

[将数据包转发到物理网络适配器](forwarding-packets-to-physical-network-adapters.md)

[管理发往物理网络适配器的 OID 请求](managing-oid-requests-to-physical-network-adapters.md)

[管理物理网络适配器发出的 NDIS 状态指示](managing-ndis-status-indications-from-physical-network-adapters.md)

 

 





