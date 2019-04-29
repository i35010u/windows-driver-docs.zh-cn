---
title: 激活 VC
description: 激活 VC
ms.assetid: 93bac975-3c9c-424b-a815-b1589b703fb5
keywords:
- 虚拟连接 WDK 的 CoNDIS，激活
- 激活虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef37c5890defea210427ea7e1a37e026030a2a2d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367956"
---
# <a name="activating-a-vc"></a>激活 VC





创建 (VC) 的虚拟连接之后 (请参阅[创建 VC](creating-a-vc.md))，则必须激活之前可以传输或对其接收数据。 呼叫管理器通过调用启动的激活 VC [ **NdisCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561649)（请参阅下图）。

![说明启动 vc 激活呼叫管理器的关系图](images/cm-07.png)

MCM 驱动程序通过调用启动的激活 VC [ **NdisMCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562792)（请参阅下图）。

![说明启动 vc 激活的 mcm 驱动程序的关系图](images/fig1-07.png)

呼叫管理器或 MCM 驱动程序在本地客户端或远程方已成功协商该 VC 的调用参数中的更改，无法启动的活动 VC 重新激活 (请参阅[Client-Initiated 请求关闭调用](client-initiated-request-to-close-a-call.md)和[传入请求，更改调用参数](incoming-request-to-change-call-parameters.md))。 呼叫管理器或 MCM 驱动程序可以调用**Ndis (M) CmActivateVc**许多次，以便单个 VC 更改已经处于活动调用的调用参数。

对于客户端发起传出呼叫，呼叫管理器或 MCM 驱动程序通常调用**Ndis (M) CmActivateVc**紧跟确认与在远程目标调用的或成功的协商的协议的数据包交换调用安装程序在交换机上。 呼叫管理器或 MCM 驱动程序调用**Ndis (M) CmActivateVc**通知使用 NDIS （和客户端） 的传出调用完成之前**Ndis (M) CmMakeCallComplete**(请参阅[进行调用](making-a-call.md)). 对于传入呼叫、 呼叫管理器或 MCM 驱动程序通常调用**Ndis (M) CmActivateVc**它被称为后**NdisCo (MCm) CreateVc**成功并在它之前调用**Ndis(M)CmDispatchIncomingCall**(请参阅[，该值指示传入调用](indicating-an-incoming-call.md))。

呼叫管理器调用**NdisCmActivateVc** NDIS 调用将导致[ **MiniportCoActivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559351)基础微型端口驱动程序的函数。 *MiniportCoActivateVc*必须验证此 VC 以验证该适配器可以支持该请求的调用的调用参数。 如果调用参数可接受的*MiniportCoActivateVc*与其适配器进行通信所需准备适配器接收或通过虚拟连接传输数据 （例如，编程接收缓冲区）。 如果不能支持请求的调用参数，微型端口驱动程序会使请求失败。

*MiniportCoActivateVc*可以同步或异步完成。 在调用[ **NdisMCoActivateVcComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563558) NDIS 调用管理器的调用将导致[ **ProtocolCmActivateVcComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570238)函数。 *ProtocolCmActivateVcComplete*必须检查返回的状态**NdisMCoActivateVcComplete**以确保成功激活虚拟连接。 如果微型端口驱动程序未成功激活 VC，呼叫管理器必须尝试通过 VC 进行通信。 *ProtocolCmActivateVcComplete*还必须完成以确保虚拟连接准备好进行数据传输之前将控制权返还给 NDIS 网络媒体所需的任何处理。

对 MCM 驱动程序调用**NdisMCmActivateVc**通知 NDIS，它已设置新创建的 VC 的调用和媒体参数或更改已建立 VC 的调用参数。 此操作会通知 NDIS，MCM 驱动程序已做好相应的 NIC 的 VC 上传输。 NDIS 通过调用在 MCM 驱动程序来完成激活序列*ProtocolCmActivateVcComplete*函数。

MCM 驱动程序调用**NdisMCmActivateVc**激活仅 VCs 用于传输和/或接收客户端数据，但不是能激活 VCs 用于如交换 MCM 驱动程序和网络组件之间的信号消息切换。 MCM 驱动程序将激活信号 VC 内部而不会调用任何**Ndis * Xxx*** 函数。 因此，是不透明的 NDIS MCM 驱动程序设置，用于自己的信号目的任何 VC。

 

 





