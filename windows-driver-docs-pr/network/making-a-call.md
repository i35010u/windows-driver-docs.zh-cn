---
title: 进行调用
description: 进行调用
ms.assetid: b5273df1-b99f-415c-a099-16a51f3329ee
keywords:
- 调用安装 WDK 的 CoNDIS
- 进行呼叫 WDK 的 CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00250ab411fc4859bd05f1f960739f23ef9356b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554993"
---
# <a name="making-a-call"></a>进行调用





下图显示了客户端管理器发出的传出调用通过调用。

![说明客户端管理器发出的传出调用通过调用关系图](images/cm-11.png)

下图显示了客户端进行传出调用通过 MCM 驱动程序。

![说明客户端进行传出调用通过 mcm 驱动程序的关系图](images/fig1-11.png)

传出调用前，必须面向连接的客户端：

-   初始化类型的结构中的调用参数[**共同\_调用\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff545384)。 呼叫管理器或 MCM 驱动程序通常使用调用参数在客户端指定的调用，而派生的微型端口驱动程序使用的媒体参数。

-   启动[创建 VC](creating-a-vc.md)与[ **NdisCoCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561696)。

在成功返回的**NdisCoCreateVc**，客户端调用[ **NdisClMakeCall** ](https://msdn.microsoft.com/library/windows/hardware/ff561635)来启动调用 （请参阅本部分中的两个图）。

对其调用中**NdisClMakeCall**，客户端将指针传递给产生的 CO\_调用\_以前初始化的参数结构。 客户端还会传递*NdisVcHandle* (返回由**NdisCoCreateVc**)，它标识在调用的 VC 的客户端将传输 （和可能是接收） 数据。 如果客户端发出的多点调用 （对多个远程方的调用），它还会将*ProtocolPartyContext* ，它指定客户端维护每个参与方的客户端分配驻留的上下文区域的句柄在 multipoint VC 的初始参与方的状态。

在调用**NdisClMakeCall**会导致此请求转发到的 NDIS [ **ProtocolCmMakeCall** ](https://msdn.microsoft.com/library/windows/hardware/ff570246)呼叫管理器或客户端与之共享的 MCM 驱动程序的函数给定*NdisVcHandle* 。 *ProtocolCmMakeCall*必须验证客户端设置的输入的调用参数。

*ProtocolCmMakeCall*与网络控制的设备建立的通信 （信号消息交换）。 呼叫管理器调用[ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)若要启动此类交换 (请参阅[发送 NET\_CoNDIS 驱动程序缓冲区结构](sending-net-buffer-structures-from-condis-drivers.md))。 MCM 驱动程序永远不会调用**NdisCoSendNetBufferLists**。 相反，它可以直接在网络上传输数据。

呼叫管理器或 MCM 驱动程序可以与相关的网络组件协商时修改客户端提供调用参数和可以返回不同的通信参数不是客户端最初提供给**NdisClMakeCall**（请参阅[传入请求，更改调用参数](incoming-request-to-change-call-parameters.md))。

使用显式*NdisPartyHandle*传递给*ProtocolCmMakeCall*指示客户端创建 VC 将用于多点调用。 呼叫管理器或 MCM 驱动程序必须分配并初始化维护每个参与方的状态信息和控制的多点调用所需的所有必要的资源。

呼叫管理器已完成与所需的其介质其网络硬件的所有必要通信后，它必须调用[ **NdisCmActivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561649)启动[VC 激活](activating-a-vc.md)上的调用发送和可能是接收数据。 MCM 驱动程序必须调用[ **NdisMCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562792)。

准备好进行 VC （即，具有 VC 后已激活） 上的数据传输基础微型端口驱动程序时，调用管理器会调用[ **NdisCmMakeCallComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561677)，和 MCM 驱动程序调用[ **NdisMCmMakeCallComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563544)。 此时，应与网络建立调用参数为 VC，协商呼叫管理器或 MCM 驱动程序和基础微型端口驱动程序应该已完成的 VC 激活。

在调用**Ndis (M) CmMakeCallComplete**，呼叫管理器或 MCM 驱动程序调用向传递参数，为 VC 作为指针类型共同的结构\_调用\_参数。 如果呼叫管理器已修改客户端最初指定的调用参数，它可以通过设置调用通知客户端\_参数\_CHANGED 标志中产生的 CO\_调用\_参数结构。

调用**Ndis (M) CmMakeCallComplete** NDIS 调用将导致[ **ProtocolClMakeCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570232)发起传出呼叫的客户端函数。 调用*ProtocolClMakeCallComplete*指示呼叫管理器已完成处理客户端的请求建立与虚拟连接**NdisClMakeCall**。

如果客户端尝试建立传出调用是否成功， *ProtocolClMakeCallComplete*应检查在调用\_参数\_CHANGED 标志以确定是否调用参数最初客户端指定已修改。 如果设置了标志，指示更改了调用参数，请*ProtocolClMakeCallComplete*应检查返回的调用参数，以确定它们是否可接受此连接。

如果调用参数可接受的*ProtocolClMakeCallComplete*只需返回控件。 如果调用参数不接受的并且如果信号协议允许重新协商此时，客户端可以调用[ **NdisClModifyCallQoS** ](https://msdn.microsoft.com/library/windows/hardware/ff561636)请求调用的参数 （请参阅中的更改[Client-Initiated 关闭调用请求](client-initiated-request-to-close-a-call.md))。 如果信号协议不允许的不可接受的调用参数的重新协商*ProtocolClMakeCallComplete*必须关闭使用调用**NdisClCloseCall**（请参阅 Client-Initiated 请求到关闭调用）。

 

 





