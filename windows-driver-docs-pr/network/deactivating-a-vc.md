---
title: 停用 VC
description: 停用 VC
keywords:
- 虚拟连接 WDK CoNDIS，停用
- 停用虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 212c6e9cb46584daca99c3b7adf131394a760707
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814989"
---
# <a name="deactivating-a-vc"></a>停用 VC





呼叫管理器调用 [**NdisCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) 作为关闭传出或传入呼叫的关键步骤，通常在数据包与泪水调用的网络组件交换之后 (参阅 [客户端启动的请求，以关闭调用](client-initiated-request-to-close-a-call.md) 和 [传入请求以关闭调用](incoming-request-to-close-a-call.md)) 。 MCM 驱动程序通过调用 [**NdisMCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc)来执行相同的操作。

调用 **NdisCmDeactivateVc** 会导致 NDIS 调用基础微型端口驱动程序的 [**MiniportCoDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_deactivate_vc) 函数 (参阅下图) 。 *MiniportCoDeactivateVc* 与其网络适配器通信，以终止此 VC (的所有通信，例如，清除适配器) 上的接收或发送缓冲区。

![说明启动 vc 停用的调用管理器的关系图](images/cm-08.png)

在停用 VC 之前，微型端口驱动程序必须在 VC 上完成任何挂起的传输。 也就是说，微型端口驱动程序必须等待，直到它完成所有发送过程，并将其指示的所有接收数据包返回给它。 停用 VC 后，微型端口驱动程序无法指示 VC 上的接收或传输发送。

请注意， *MiniportCoDeactivateVc* 不会删除 VC。 Creator (客户端、调用管理器或 MCM 驱动程序) ，不会重复使用的特定 VC 调用 [**NdisCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscodeletevc) [销毁该 vc](deleting-a-vc.md)。 已停用的 VC 可以通过面向连接的客户端、呼叫管理器或 MCM 驱动程序 [重新激活](activating-a-vc.md) 。

*MiniportCoDeactivateVc* 可以同步或异步完成。 对 [**NdisMCoDeactivateVcComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcodeactivatevccomplete)的调用。 使 NDIS 调用最初请求 VC 停用的调用管理器的 [**ProtocolCmDeactivateVcComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_deactivate_vc_complete) 函数。 完成停用意味着在激活时使用的 VC 的所有调用参数都将不再有效。 禁止对 VC 的任何进一步使用，除非使用一组新的调用参数重新激活它。

MCM 驱动程序对 **NdisMCmDeactivateVc** 的调用告知 NDIS 它已停用某个 vc，或更改已建立的 vc 上的调用参数 (参见下图) 。 NDIS 通过调用 MCM 驱动程序的 *ProtocolCmDeactivateVcComplete* 函数来完成停用序列。

![阐释 mcm 驱动程序启动 vc 停用的示意图](images/fig1-08.png)

MCM 驱动程序未调用 **NdisMCmDeactivateVc** 来停用 VCs，用于在 MCM 驱动程序和网络组件（例如交换机）之间交换信号消息。 MCM 驱动程序在内部停用信号 VC，无需调用任何 **Ndis * Xxx*** 函数。

 

