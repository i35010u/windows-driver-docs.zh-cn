---
title: 呼叫
description: 呼叫
ms.assetid: b5273df1-b99f-415c-a099-16a51f3329ee
keywords:
- 调用设置 WDK CoNDIS
- 拨打 WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6956556adad86bef889f2d9fa0b2efb7ce39bce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844132"
---
# <a name="making-a-call"></a>呼叫





下图显示了通过呼叫管理器发出传出呼叫的客户端。

![演示通过呼叫管理器发出传出呼叫的客户端的关系图](images/cm-11.png)

下图显示了通过 MCM 驱动程序发出传出呼叫的客户端。

![说明通过 mcm 驱动程序发出传出呼叫的客户端的关系图](images/fig1-11.png)

发出传出呼叫之前，面向连接的客户端必须：

-   初始化类型为[**CO\_调用\_参数**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545384(v=vs.85))的结构中的调用参数。 调用管理器或 MCM 驱动程序通常使用客户端指定的调用参数来设置呼叫，并使用这些参数来派生用于微型端口驱动程序的媒体参数。

-   使用[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)开始[创建 VC](creating-a-vc.md) 。

成功返回**NdisCoCreateVc**时，客户端会调用[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)来启动调用（请参阅本部分中的两个数字）。

在调用**NdisClMakeCall**时，客户端会传递一个指向 CO\_调用的指针\_先前初始化的参数结构。 客户端还传递*NdisVcHandle* （由**NdisCoCreateVc**返回），该程序标识了客户端将在其上传输（并可能接收）调用的数据的 VC。 如果客户端进行 multipoint 调用（调用多个远程方），则它还会传递一个*ProtocolPartyContext* ，它指定客户端分配的常驻上下文区域的句柄，在该区域中，客户端将维护初始的每个参与方状态multipoint VC 上的参与方。

对**NdisClMakeCall**的调用会使 NDIS 将此请求转发到调用管理器或 MCM 驱动程序的[**ProtocolCmMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_make_call)函数，客户端在该驱动程序中共享给定的*NdisVcHandle* 。 *ProtocolCmMakeCall*必须验证客户端设置的输入调用参数。

*ProtocolCmMakeCall*通过网络控制设备进行连接以建立连接。 调用管理器调用[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists)来启动此类交换（请参阅[通过 CoNDIS 驱动程序发送 NET\_缓冲区结构](sending-net-buffer-structures-from-condis-drivers.md)）。 MCM 驱动程序绝不会调用**NdisCoSendNetBufferLists**。 相反，它会直接通过网络传输数据。

调用管理器或 MCM 驱动程序可以在与相关的网络组件协商时修改客户端提供的调用参数，并可以返回不同于客户端最初提供给**NdisClMakeCall**的流量参数（请参阅[传入请求更改调用参数](incoming-request-to-change-call-parameters.md)）。

传递给*ProtocolCmMakeCall*的显式*NdisPartyHandle*表示客户端创建的 VC 将用于 multipoint 调用。 调用管理器或 MCM 驱动程序必须分配和初始化维护每方状态信息和控制 multipoint 调用所需的任何必要资源。

在呼叫管理器按介质介质的要求完成与其网络硬件的所有必要通信后，必须调用[**NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc)来启动对将在其上发送和接收调用数据的[VC 的激活](activating-a-vc.md)。 MCM 驱动程序必须调用[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc)。

当基础微型端口驱动程序准备好在 VC 上进行数据传输时（即，在启用 VC 后），调用管理器将调用[**NdisCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmakecallcomplete)，而 MCM 驱动程序调用[**NdisMCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmakecallcomplete)。 此时，调用管理器或 MCM 驱动程序应该已与网络协商，以便为 VC 建立调用参数，基础微型端口驱动程序应已完成 VC 的激活。

在调用**Ndis （M） CmMakeCallComplete**时，调用管理器或 MCM 驱动程序会将 VC 的 call 参数传递为指向类型为 CO\_调用的结构的指针\_参数。 如果调用管理器已修改客户端最初指定的调用参数，则它可以通过在 CO\_调用\_参数结构中设置调用\_参数\_CHANGED 标志来通知客户端。

调用**ndis （M） CmMakeCallComplete**会使 ndis 调用发起传出调用的客户端的[**ProtocolClMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_make_call_complete)函数。 对*ProtocolClMakeCallComplete*的调用指示调用管理器已完成处理客户端的请求，以便与**NdisClMakeCall**建立虚拟连接。

如果客户端尝试建立传出调用成功， *ProtocolClMakeCallComplete*应检查调用\_参数\_CHANGED 标志，以确定客户端最初指定的调用参数是否为时间. 如果设置了标志，指示调用参数已更改，则*ProtocolClMakeCallComplete*应检查返回的调用参数，以确定它们是否可用于此连接。

如果调用参数是可接受的， *ProtocolClMakeCallComplete*只会返回 control。 如果调用参数不可接受，并且信号协议此时允许重新协商，则客户端可以调用[**NdisClModifyCallQoS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmodifycallqos)来请求调用参数的更改（请参阅[客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md)）。 如果信号协议不允许重新协商无法接受的调用参数，则*ProtocolClMakeCallComplete*必须使用**NdisClCloseCall**销毁调用（请参阅客户端启动的请求以关闭调用）。

 

 





