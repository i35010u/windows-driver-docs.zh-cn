---
title: 激活 VC
description: 激活 VC
ms.assetid: 93bac975-3c9c-424b-a815-b1589b703fb5
keywords:
- 虚拟连接 WDK CoNDIS，激活
- 激活虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c39f5c0f4ab02fcf7404cb6786a24d2ba15d1d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213999"
---
# <a name="activating-a-vc"></a>激活 VC





 (VC) 创建了虚拟连接后 (请参阅 [创建 vc](creating-a-vc.md)) ，必须先激活它，然后才能在其上传输或接收数据。 调用管理器通过调用 [**NdisCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc) 启动 VC 的激活 (参阅下图) 。

![说明启动 vc 激活的调用管理器的关系图](images/cm-07.png)

MCM 驱动程序通过调用 [**NdisMCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc) 启动 VC 的激活， (参见下图) 。

![阐释 mcm 驱动程序启动 vc 激活的示意图](images/fig1-07.png)

如果本地客户端或远程方成功协商了该 (VC 上调用参数的更改，则调用管理器或 MCM 驱动程序可以启动活动 VC 的重新激活，请参阅 [客户端启动的请求以关闭调用](client-initiated-request-to-close-a-call.md) ，并 [传入请求以更改调用参数](incoming-request-to-change-call-parameters.md)) 。 对于单个 VC，调用管理器或 MCM 驱动程序可以多次调用 **Ndis (M) CmActivateVc** ，以更改已经处于活动状态的调用的调用参数。

对于客户端发起的传出呼叫，呼叫管理器或 MCM 驱动程序通常会立即调用 **Ndis (M) CmActivateVc** ，并在交换机上确认与调用的远程目标的协商协议或成功的调用设置。 调用管理器或 MCM 驱动程序调用**ndis (M) CmActivateVc** ，然后再通知 ndis (，并在客户端) 使用**ndis (M**) [Making a Call](making-a-call.md) 对于传入呼叫，调用管理器或 MCM 驱动程序通常会调用 **ndis (M) CmActivateVc** ，然后在调用 **NdisCo (MCM) CreateVc** 之前，并在调用 **ndis (M) CmDispatchIncomingCall** 之前， (请参阅 [指示传入调用](indicating-an-incoming-call.md)) 。

调用管理器调用 **NdisCmActivateVc** 会导致 NDIS 调用基础微型端口驱动程序的 [**MiniportCoActivateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_activate_vc) 函数。 *MiniportCoActivateVc* 必须验证此 VC 的 call 参数，以验证适配器是否可以支持请求的调用。 如果调用参数是可接受的， *MiniportCoActivateVc* 会根据需要与其适配器进行通信，以便准备适配器，以便通过虚拟连接接收或传输数据 (例如，) 编程接收缓冲区。 如果不支持请求的调用参数，微型端口驱动程序将无法请求。

*MiniportCoActivateVc* 可以同步或异步完成。 调用 [**NdisMCoActivateVcComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoactivatevccomplete) 会导致 NDIS 调用调用管理器的 [**ProtocolCmActivateVcComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_activate_vc_complete) 函数。 *ProtocolCmActivateVcComplete* 必须检查 **NdisMCoActivateVcComplete** 返回的状态，以确保已成功激活虚拟连接。 如果微型端口驱动程序未成功激活 VC，则调用管理器不得尝试通过 VC 进行通信。 *ProtocolCmActivateVcComplete* 还必须完成网络媒体所需的任何处理，以确保虚拟连接在将控制权返回给 NDIS 之前已准备好进行数据传输。

MCM 驱动程序对 **NdisMCmActivateVc** 的调用告知 NDIS 它已在新创建的 vc 上设置调用和媒体参数，或者在已建立的 vc 上更改了调用参数。 此操作通知 NDIS MCM 驱动程序已使 NIC 准备好在 VC 上传输。 NDIS 通过调用 MCM 驱动程序的 *ProtocolCmActivateVcComplete* 函数来完成激活序列。

MCM 驱动程序调用 **NdisMCmActivateVc** 来仅激活用于传输和/或接收客户端数据的 vcs，而不是激活用于在 MCM 驱动程序和网络组件（例如交换机）之间交换信号消息的 vcs。 MCM 驱动程序在内部激活信号 VC，无需调用任何 **Ndis * Xxx*** 函数。 MCM 驱动程序为其自身的信号用途设置的任何 VC 都是不透明的。

 

