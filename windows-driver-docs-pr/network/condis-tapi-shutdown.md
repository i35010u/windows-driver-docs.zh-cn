---
title: CoNDIS TAPI 关闭
description: CoNDIS TAPI 关闭
ms.assetid: 97baf489-9a9b-48c8-b0f8-79beea33bc38
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 联网，TAPI 服务
- 台电话服务 WDK WAN，关闭
- CoNDIS TAPI WDK 网络、 关闭
- 连接网络、 关闭操作的 CoNDIS TAPI WDK
- 关闭 WDK 网络
- 关闭的 CoNDIS TAPI 操作调用 WDK 的 CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8ca8d859a555f1175c78d790e8cc5b6692b1c3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576112"
---
# <a name="condis-tapi-shutdown"></a>CoNDIS TAPI 关闭





TAPI 会话开始后的 CoNDIS WAN 的微型端口驱动程序枚举其 TAPI 功能到应用程序。 某个会话中可以打开一个或多个行，并可以建立一个或多个调用。 行是打开期间，多个调用可以是建立，然后关闭或删除。 会话期间，一个或多个行可以通过转换从转打开关闭多次。 在本部分中描述的微型端口驱动程序如何处理这样的变革。

### <a name="closing-a-call"></a>关闭调用

本地节点或远程节点，可以关闭进程内调用。 在调用可以关闭本地节点上或者因为最后一个句柄为应用程序调用已关闭句柄，或可能是因为微型端口驱动程序[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)或[*MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)已调用。 如果远程节点将挂起的进程内调用，微型端口驱动程序必须通知上层中断调用。

如果在调用关闭本地节点上的应用程序，它必须断开呼叫。 调用已断开连接由于应用程序调用 TAPI **lineDrop**函数。 此 TAPI 函数调用将导致 NDPROXY 驱动程序调用[ **NdisClCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561627)函数，并以传递的句柄，表示调用 VC。 NDIS 反过来调用的 CoNDIS WAN 微型端口驱动程序[ **ProtocolCmCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570241)函数。 微型端口驱动程序应返回 NDIS\_状态\_NDPROXY 因此微型端口驱动程序可以完成的 PENDING **NdisClCloseCall**以异步方式。

微型端口驱动程序*ProtocolCmCloseCall*必须与网络控制设备终止本地节点和远程节点之间的连接进行通信。 然后，微型端口驱动程序必须调用[ **NdisMCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562818)函数启动的调用使用 VC 停用。

微型端口驱动程序终止连接后其*ProtocolCmCloseCall*可以调用[ **NdisMCmCloseCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562803)函数来完成调用闭包。

如果远程节点将挂起的进程内调用，微型端口驱动程序会调用[ **NdisCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561670)函数来通知 NDISWAN 和 NDPROXY 关闭传入呼叫。

### <a name="closing-a-line"></a>关闭的行

行已关闭时打开的句柄到行的上次应用已关闭句柄。 由于调用 TAPI 的应用程序关闭一行**lineClose**函数。 此 TAPI 函数调用将导致 NDPROXY 驱动程序启动的该行上的所有调用的闭包，在上一部分中所述。 微型端口驱动程序应删除这些调用，并清除其状态。

### <a name="closing-a-session"></a>关闭会话

可以通过上层或 CoNDIS WAN 的微型端口驱动程序来启动会话终止。 最后一个客户端进程已从更高级别的电话服务模块分离后，系统将通知 NDPROXY 驱动程序，它必须终止它与每个已注册适配器的会话。 若要执行此操作，NDPROXY 驱动程序调用[ **NdisClCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff561626)函数，并将该句柄传递给 TAPI 地址族。 NDIS 反过来调用微型端口驱动程序[ **ProtocolCmCloseAf** ](https://msdn.microsoft.com/library/windows/hardware/ff570240)函数。 微型端口驱动程序应终止它具有在指定适配器上的正在进行中的任何相关的活动并释放任何相关资源。 在调用**NdisClCloseAddressFamily**，客户端应考虑到 TAPI 地址系列无效句柄。

如果正在卸载微型端口驱动程序中，则会发生驱动程序启动的会话终止其*MiniportHaltEx*函数。 通常情况下，微型端口驱动程序将完成所有未完成的 NDPROXY 请求并通知 NDISWAN 所有调用将都关闭。 如果已再次以后重新加载微型端口驱动程序，它会转完成前面所述相同的初始化过程。

如果发生了一些需要完成重新初始化所有客户端和驱动程序的动态重新配置的 CoNDIS WAN 微型端口驱动程序可能也会启动会话终止。 例如，如果适配器的线路设备 （例如，支持的线路设备数） 建模已更改动态。

 

 





