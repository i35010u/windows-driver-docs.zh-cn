---
title: 关闭调用传入请求
description: 关闭调用传入请求
ms.assetid: ecdcb74d-6151-4e2b-8fe7-95f455f4deb4
keywords:
- 关闭调用时传入请求 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5093c65717a634b159e8812c4324dc4df6d61c37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554925"
---
# <a name="incoming-request-to-close-a-call"></a>关闭调用传入请求





当远程客户端关闭调用时，本地呼叫管理器或 MCM 驱动程序必须指示对本地客户端传入的请求。 若要指示此类请求，调用管理器会调用[ **NdisCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561670)与*CloseStatus*设置为 NDIS\_状态\_成功 （请参阅下图）。

![说明通过调用管理器的传入请求，以关闭调用关系图 ](images/cm-22.png)

MCM 驱动程序调用[ **NdisMCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff563541)以指示传入的请求关闭调用 （请参阅下图）。

![说明通过 mcm 驱动程序的传入请求，以关闭调用关系图 ](images/fig1-22.png)

呼叫管理器或 MCM 驱动程序还可以调用**Ndis (M) CmDispatchIncomingCloseCall**:

-   从其[ **ProtocolCmIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570245)函数如果确定面向连接的客户端正在请求中调用以响应传入调用的参数不能接受更改以前，将由呼叫管理器或 MCM 驱动程序 (请参阅[对更改调用参数的传入请求](incoming-request-to-change-call-parameters.md))。

-   如果异常网络条件强制关闭活动调用的调用管理器。

在调用**Ndis (M) CmDispatchIncomingCloseCall** NDIS 调用将导致[ **ProtocolClIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570230)面向连接的客户端上的函数连接。 *ProtocolClIncomingCloseCall*应执行任何协议确定的操作，例如通知其自己的客户端或客户端在断开连接。 如果要关闭的调用是由客户端，创建 multipoint VC *ProtocolClIncomingCloseCall*必须调用[ **NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)直到一个参与方的一个或多个时间将保留在 VC (请参阅[Multipoint 调用正在删除参与方](dropping-a-party-from-a-multipoint-call.md))。

*ProtocolClIncomingCloseCall*然后，必须调用[ **NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627)（使用的句柄上 VC VC 是否由客户端创建 multipoint VC 的最后一个参与方） 以确认的客户端将无法再尝试发送或收到此特定 VC 上的数据。 如果呼叫管理器或 MCM 驱动程序创建此 VC *ProtocolClIncomingCloseCall*应返回控制后将调用**NdisClCloseCall**。 呼叫管理器或 MCM 驱动程序必须停用 VC (请参阅[停用 VC](deactivating-a-vc.md))。

如果客户端最初创建的传出调用此 VC 并*CloseStatus*是 NDIS\_状态\_成功后， *ProtocolClIncomingCloseCall*可以根据需要关闭 VC与[ **NdisCoDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff561698)(请参阅[删除 VC](deleting-a-vc.md)) 或重复使用的另一个调用 VC。 如果*CloseStatus*不是 NDIS\_状态\_成功后， *ProtocolClIncomingCloseCall*必须调用**NdisCoDeleteVc**。

如果呼叫管理器或 MCM 驱动程序最初可以选择创建的传入呼叫、 呼叫管理器或 MCM 驱动程序可以为此 VC[删除 VC](deleting-a-vc.md)通过分别调用**NdisCoDeleteVc**或[**NdisMCmDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff562819)。

 

 





