---
title: 删除 VC
description: 删除 VC
ms.assetid: 6e49fb69-0b22-4f52-9b6d-661e818c1758
keywords:
- 虚拟连接 WDK 的 CoNDIS，删除
- 正在删除虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c1d6067574130e5e7d79230194b1a56a11ee2ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347511"
---
# <a name="deleting-a-vc"></a>删除 VC





面向连接的客户端、 呼叫管理器或启动的虚拟线路 (VC) 创建的 MCM 驱动程序可以启动该 VC 的删除。 客户端因此删除 VC 它之前创建的传出呼叫、 呼叫管理器或 MCM 驱动程序删除它之前为创建的传入呼叫通过网络，VC 并呼叫管理器删除它之前创建用于交换信号 VC在网络上的消息。 （MCM 驱动程序不会调用 NDIS 以删除它创建信号消息交换的 VC。 MCM 驱动程序将删除此类使用的内部操作，则不透明的 NDIS VC。）

面向连接的客户端或调用管理器会启动删除的与 VC [ **NdisCoDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff561698)。

下图显示的某调用的客户端的 VC 删除启动管理器。

![说明的 vc 删除启动呼叫管理器的客户端的关系图](images/cm-09.png)

下图显示了启动 VC 删除 MCM 驱动程序的客户端。

![说明的 vc 删除启动 mcm 驱动程序的客户端的关系图](images/fig1-09.png)

下图显示调用的 VC 删除启动管理器。

![说明的 vc 删除启动呼叫管理器的关系图](images/cm-10.png)

当客户端或调用管理器调用**NdisCoDeleteVc**或当 MCM 驱动程序调用**NdisMCmDeleteVc**，给定 VC 上必须有任何未完成的调用，必须已被 VC [停用](deactivating-a-vc.md)。 若要满足这些要求意味着满足以下条件：

-   已调用客户端[ **NdisClCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561627)与给定*NdisVcHandle*并将其[close 调用请求](client-initiated-request-to-close-a-call.md)已完成已成功。

-   已调用呼叫管理器[ **NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657)或已调用 MCM 驱动程序[ **NdisMCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562818)与给定*NdisVcHandle*和停用请求已成功完成 (请参阅[传入请求，关闭调用](incoming-request-to-close-a-call.md))。

客户端或调用 manager 调用**NdisCoDeleteVc** NDIS 调用这两个基础微型端口驱动程序将导致[ **MiniportCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559358)函数并[ **ProtocolCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570253)函数的调用方与其共享的客户端或调用管理器*NdisVcHandle* （请参阅前面的三个数字）。

*MiniportCoDeleteVc*释放为 VC 分配为 VC，微型端口驱动程序的上下文的任何资源。 *ProtocolCoDeleteVc*版本为 VC 状态的客户端或调用管理器用来执行操作，并跟踪任何资源。 这两*MiniportCoDeleteVc*并*ProtocolCoDeleteVc*是不能返回 NDIS 同步函数\_状态\_PENDING。

MCM 驱动程序将启动删除的与 VC [ **NdisMCmDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff562819)（请参阅下图）。

![说明的 vc 删除启动 mcm 驱动程序的关系图 ](images/fig1-10.png)

MCM 驱动程序调用**NdisMCmDeleteVc** NDIS 调用将导致[ **ProtocolCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570253)函数的客户端与 MCM 驱动程序共享*NdisVcHandle* 。

当**NdisCoDeleteVc**或**NdisMCmDeleteVc**控件，将返回*NdisVcHandle*不再有效。

 

 





