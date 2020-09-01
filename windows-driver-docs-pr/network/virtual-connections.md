---
title: 虚拟连接
description: 虚拟连接
ms.assetid: becb3acf-2a23-408a-8d1f-ff8a1e7ffe61
keywords:
- 面向连接的 NDIS WDK，虚拟连接
- CoNDIS WDK 网络，虚拟连接
- 虚拟连接 WDK CoNDIS
- 虚拟连接 WDK CoNDIS，关于虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76c1152efb95646d4f0d93239aba9786bd1933f8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218304"
---
# <a name="virtual-connections"></a>虚拟连接





在本地计算机上， * (VC) 的虚拟连接 * 是一个终结点 (或关联) ，它可以在客户端、调用管理器、MCM 驱动程序和微型端口驱动程序之间托管单个调用。 在网络上，VC 指两个通信终结点之间的连接，例如两个面向连接的客户端。

许多 VCs 在 NIC 上可以同时处于活动状态，从而使 NIC 同时为多个调用服务。 每个连接可以连接到不同计算机上的不同终结点。

网络上的 VCs 因其提供给客户端的服务类型而异。 例如，VC 可以提供单向或双向服务。 服务质量 (QoS) 每个方向的参数可以保证特定的性能阈值，例如带宽和延迟时间。 根据信号协议，VC 的 QoS 可转让。 有关对 QoS 的 NDIS 支持的详细信息，请参阅 [服务质量](quality-of-service.md)。

网络上的 VC 可以是交换式 VC (SVC) 或永久 VC (PVC) ：

-   根据特定调用的需要创建 SVC。 例如，面向连接的客户端为要进行的传出呼叫启动创建 VC。 同样，调用管理器或 MCM 驱动程序会启动为传入调用创建 VC，并向面向连接的客户端指示。 调用管理器或 MCM 驱动程序必须通信，有时会与远程方协商 VC 的参数。

-   永久 VC 是手动创建的，并最终由运算符使用在 NDIS 中未提供的配置实用工具删除。 监视这种手动创建和删除 Pvc 的客户端可以使用 [OID \_ co \_ ADD \_ pvc](./oid-co-add-pvc.md) 和 [OID \_ co \_ DELETE \_ pvc](./oid-co-delete-pvc.md) oid 来请求调用管理器或 MCM 驱动程序在其已配置的 pvc 列表中添加或删除 PVC。 PVC 的 QoS 由操作员配置，无法通过网络进行流通。

在 NDIS 中，VC 由微型端口驱动程序分配的资源组成，用于维护有关网络上的 VC 的状态信息。 这些资源可能包括但不限于内存缓冲区、事件和数据结构。 要求使用微型端口驱动程序为一个连接的客户端创建用于传出呼叫的和呼叫管理器的 VC 的此类上下文。 有关创建 VCs 的详细信息，请参阅 [创建 VC](creating-a-vc.md)。

在创建的 VC 可用于数据传输之前，必须通过调用管理器或 MCM 驱动程序将其激活。 若要激活 VC，微型端口驱动程序或 MCM 驱动程序将设置 VC 的资源，并根据需要与 NIC 通信，以便准备 NIC 以在 VC 上接收或传输数据。 有关 VC 激活的详细信息，请参阅 [激活 vc](activating-a-vc.md)。

当拆开调用时，呼叫管理器或 MCM 驱动程序会停用用于调用的 [VC](deactivating-a-vc.md) 。

断开呼叫后，VC 的创建者 (面向连接的客户端、调用管理器或 MCM 驱动程序) 可以启动 [删除 VC](deleting-a-vc.md) 或将 vc 用于另一次调用。

 

