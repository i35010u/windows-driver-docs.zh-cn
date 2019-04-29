---
title: 客户端发起的结束呼叫请求
description: 客户端发起的结束呼叫请求
ms.assetid: 1eb9c898-086a-463f-a4ae-d5a8727f7d73
keywords:
- 客户端启动关闭调用时请求 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 861f3bb40037029df78e7e17fc4ad76e12cde3a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373145"
---
# <a name="client-initiated-request-to-close-a-call"></a>客户端发起的结束呼叫请求





如果客户端即将关闭 multipoint 调用仍连接到多个参与方，必须首先调用[ **NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)尽可能多地从调用 （请参阅必要到放置所有，但最后一个参与方[从 Multipoint 调用删除参与方](dropping-a-party-from-a-multipoint-call.md))。

客户端启动与调用的右[ **NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627)。 下图显示了客户端发起的呼叫管理器通过调用结束。

![说明客户端发起的呼叫管理器通过调用结束的关系图](images/cm-20.png)

下图显示了客户端启动关闭通过 MCM 驱动程序的调用。

![说明客户端启动关闭通过 mcm 驱动程序的调用关系图](images/fig1-20.png)

面向连接的客户端通常会调用**NdisClCloseCall**的任何一种方法在下列情况：

-   若要关闭的已建立传出或传入呼叫。

-   从[ **ProtocolClIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570230)函数来关闭已建立的调用 (请参阅[传入的请求，以关闭调用](incoming-request-to-close-a-call.md))。

-   从[ *ProtocolClIncomingCallQoSChange* ](https://msdn.microsoft.com/library/windows/hardware/ff570229)函数，如果远程方提出建议的 QoS 更改是不可接受的中断已建立的调用 (请参阅[更改传入请求调用参数](incoming-request-to-change-call-parameters.md))。

-   从[ **ProtocolClModifyCallQoSComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570233)函数来关闭已建立的调用，则远程方无法接受客户端提出了 QoS 更改 (请参阅[Client-Initiated 请求以更改调用参数](client-initiated-request-to-change-call-parameters.md))。

客户端的调用**NdisClCloseCall** NDIS 调用管理器的调用或 MCM 驱动程序将导致[ **ProtocolCmCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570241)函数。 *ProtocolCmCloseCall*必须与网络控制设备终止本地节点和远程节点之间的连接进行通信。

如果*ProtocolCmCloseCall*传递显式*CallMgrPartyContext*，正在终止的调用是多点调用。 呼叫管理器或 MCM 驱动程序必须执行与网络硬件，根据其媒体类型，若要终止与 multipoint 调用调用的任何必要的网络通信。

可以传递 NDIS *ProtocolCmCloseCall*指向包含对的调用中的客户端提供数据的缓冲区的指针**NdisClClose**。 此数据可以是指示在调用已关闭的原因的诊断数据或信号协议所需的任何其他数据。 *ProtocolCmCloseCall*之前必须发送任何此类数据通过网络完成调用终止。 如果不支持将数据发送并发与被终止的连接，呼叫管理器或 MCM 驱动程序应返回 NDIS\_状态\_无效\_数据。

*ProtocolCmCloseCall*可以使用完成同步或者，更可能，以异步方式[ **NdisCmCloseCallComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561655)（对于呼叫管理器） 或[ **NdisMCmCloseCallComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562803)（对于 MCM 驱动程序）。 调用**Ndis (M) CmCloseCallComplete**会导致调用客户端的 NDIS [ **ProtocolClCloseCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570225)函数。

呼叫管理器或 MCM 驱动程序必须启动停用的用于通过分别调用调用 VC [ **NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657)或[ **NdisMCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562818)(请参阅[停用 VC](deactivating-a-vc.md))。 VC （客户端、 呼叫管理器或 MCM 驱动程序） 的创建者可以根据需要故障删除 VC (请参阅[删除 VC](deleting-a-vc.md))。

 

 





