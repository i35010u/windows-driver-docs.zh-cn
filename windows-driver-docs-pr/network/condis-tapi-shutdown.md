---
title: CoNDIS TAPI 关闭
description: CoNDIS TAPI 关闭
ms.assetid: 97baf489-9a9b-48c8-b0f8-79beea33bc38
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，TAPI 服务
- telephonic services WDK WAN，shutdown
- CoNDIS TAPI WDK 网络，关闭
- CoNDIS TAPI WDK 网络，关闭操作
- 关闭 WDK 网络
- 关闭 CoNDIS TAPI 操作会调用 WDK CoNDIS WAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4f96cffeaaf4b8f9e22cc3109e3496f4685fffd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209793"
---
# <a name="condis-tapi-shutdown"></a>CoNDIS TAPI 关闭





在 CoNDIS WAN 微型端口驱动程序对应用程序的 TAPI 功能进行枚举后，就会开始 TAPI 会话。 在会话中，可以打开一条或多条线路，并且可以建立一个或多个调用。 在行处于打开状态时，可以建立并关闭或删除多个调用。 在会话过程中，一个或多个行可以通过打开的转换多次关闭。 此部分介绍了微型端口驱动程序如何处理此类转换。

### <a name="closing-a-call"></a>结束调用

进程内调用可以通过本地节点或远程节点关闭。 此调用可以在本地节点上关闭，这可能是因为最后一个应用程序的调用已经关闭了句柄，也可能是因为已调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 或 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 。 如果远程节点挂断进程内调用，微型端口驱动程序必须通知上层，使其能够断开呼叫。

如果本地节点上的应用程序关闭调用，则必须断开呼叫。 由于应用程序调用了 TAPI **lineDrop** 函数，因此调用已断开连接。 此 TAPI 函数调用会导致 NDPROXY 驱动程序调用 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) 函数并传递表示调用的 VC 的句柄。 NDIS 反过来调用 CoNDIS WAN 微型端口驱动程序的 [**ProtocolCmCloseCall**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_close_call) 函数。 微型端口驱动程序应 \_ 将 NDIS 状态返回 \_ 到 NDPROXY，以便微型端口驱动程序可以异步完成 **NdisClCloseCall** 。

微型端口驱动程序的 *ProtocolCmCloseCall* 必须与网络控制设备通信，以终止本地节点和远程节点之间的连接。 然后，微型端口驱动程序必须调用 [**NdisMCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc) 函数以启动用于调用的 VC 的停用。

微型端口驱动程序终止连接后，其 *ProtocolCmCloseCall* 可以调用 [**NdisMCmCloseCallComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmclosecallcomplete) 函数来完成调用闭包。

如果远程节点挂断进程内调用，微型端口驱动程序将调用 [**NdisCmDispatchIncomingCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall) 函数，通知 NDISWAN 和 NDPROXY 解除传入呼叫。

### <a name="closing-a-line"></a>右行

当最后一个应用程序的打开句柄已关闭该句柄时，将关闭该行。 由于调用了 TAPI **lineClose** 函数的应用程序的结果，行被关闭。 此 TAPI 函数调用导致 NDPROXY 驱动程序启动对该行的所有调用的关闭，如前一部分中所述。 微型端口驱动程序应丢弃这些调用并清除其状态。

### <a name="closing-a-session"></a>关闭会话

会话终止可以由上层或 CoNDIS WAN 微型端口驱动程序启动。 在上一个客户端进程与较高级别的电话模块分离后，将通知 NDPROXY 驱动程序必须终止与每个已注册适配器的会话。 为此，NDPROXY 驱动程序将调用 [**NdisClCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily) 函数并将句柄传递到 TAPI 地址系列。 NDIS 又调用微型端口驱动程序的 [**ProtocolCmCloseAf**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_close_af) 函数。 微型端口驱动程序应终止在指定适配器上正在进行的任何相关活动，并释放任何相关的资源。 调用 **NdisClCloseAddressFamily**之后，客户端应考虑 TAPI 地址系列的句柄无效。

如果在 *MiniportHaltEx* 函数中卸载微型端口驱动程序，则可能会发生驱动程序启动的会话终止。 通常，微型端口驱动程序会完成所有未完成的 NDPROXY 请求，并通知 NDISWAN 所有调用都正在关闭。 如果以后再次加载微型端口驱动程序，则会经历前面所述的相同初始化过程。

如果 CoNDIS WAN 微型端口驱动程序耗费一些需要完全重新初始化所有客户端和驱动程序的动态重新配置，还可能会启动会话终止。 例如，如果适配器的线路设备建模 (例如，动态变化) 支持的行设备数。

 

