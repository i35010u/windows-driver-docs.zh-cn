---
title: 删除 VC
description: 删除 VC
ms.assetid: 6e49fb69-0b22-4f52-9b6d-661e818c1758
keywords:
- 虚拟连接 WDK CoNDIS，删除
- 正在删除虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63ec0604c350817f6eafaa735a7a07682d11c70e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838180"
---
# <a name="deleting-a-vc"></a>删除 VC





只有面向连接的客户端、调用管理器或启动虚拟线路（VC）创建的 MCM 驱动程序才能启动删除该 VC。 因此，客户端会删除先前为传出调用创建的 VC，呼叫管理器或 MCM 驱动程序将删除以前为通过网络进行的传入呼叫创建的 vc，并使用呼叫管理器删除先前创建的用于交换信号的 VC通过网络发送的消息。 （MCM 驱动程序不调用 NDIS 来删除它创建用于交换信号消息的 VC。 MCM 驱动程序将使用不透明的内部操作删除此类 VC。）

面向连接的客户端或调用管理器使用[**NdisCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc)启动删除 VC。

下图显示了启动删除 VC 的呼叫管理器的客户端。

![说明启动删除 vc 的调用管理器客户端的关系图](images/cm-09.png)

下图显示了启动删除 VC 的 MCM 驱动程序的客户端。

![说明启动删除 vc 的 mcm 驱动程序的客户端的关系图](images/fig1-09.png)

下图显示了启动删除 VC 的调用管理器。

![说明调用管理器启动删除 vc 的关系图](images/cm-10.png)

当客户端或调用管理器调用**NdisCoDeleteVc**或 MCM 驱动程序调用**NdisMCmDeleteVc**时，给定 VC 上必须没有未处理的调用，并且 VC 必须已被[停用](deactivating-a-vc.md)。 为了满足这些要求，意味着满足以下条件：

-   客户端已在给定的*NdisVcHandle*中调用了[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) ，但其[结束调用请求](client-initiated-request-to-close-a-call.md)已成功完成。

-   调用管理器已调用[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) ，或者 MCM 驱动程序已通过给定的*NdisVcHandle*调用了[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc) ，并已成功完成停用请求（请参阅[传入请求到关闭呼叫](incoming-request-to-close-a-call.md)）。

客户端或调用管理器对**NdisCoDeleteVc**的调用会使 NDIS 同时调用基础微型端口驱动程序的[**MiniportCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc)函数，以及调用方将使用的客户端或调用管理器的[**ProtocolCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc)函数共享*NdisVcHandle* （请参阅前三个图形）。

*MiniportCoDeleteVc*释放为 vc 分配的任何资源，以及 vc 的微型端口驱动程序的上下文。 *ProtocolCoDeleteVc*释放客户端或调用管理器用于对 VC 执行操作和跟踪状态的任何资源。 *MiniportCoDeleteVc*和*ProtocolCoDeleteVc*都是同步函数，不能\_挂起状态返回 NDIS\_状态。

MCM 驱动程序使用[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc)启动删除 VC 的操作（见下图）。

![说明启动删除 vc 的 mcm 驱动程序的示意图 ](images/fig1-10.png)

MCM 驱动程序对**NdisMCmDeleteVc**的调用会使 NDIS 调用 MCM 驱动程序与*NdisVcHandle*共享的客户端的[**ProtocolCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc)函数。

当**NdisCoDeleteVc**或**NdisMCmDeleteVc**返回 control 时， *NdisVcHandle*不再有效。

 

 





