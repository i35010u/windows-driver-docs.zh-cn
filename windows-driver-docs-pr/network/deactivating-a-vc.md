---
title: 停用 VC
description: 停用 VC
ms.assetid: 094e339c-b5a7-4894-9a3d-145231311647
keywords:
- 虚拟连接 WDK 的 CoNDIS，停用
- 停用虚拟连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d023e8d5b173156a0efd438c052984685315659
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524665"
---
# <a name="deactivating-a-vc"></a>停用 VC





呼叫管理器调用[ **NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657)作为关闭传出或传入调用，通常后关闭调用 （请参阅与网络组件的数据包交换中的基本步骤[客户端发出的请求以关闭呼叫](client-initiated-request-to-close-a-call.md)并[传入请求，关闭调用](incoming-request-to-close-a-call.md))。 MCM 驱动程序执行同样的操作通过调用[ **NdisMCmDeactivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562818)。

在调用**NdisCmDeactivateVc**会导致调用基础微型端口驱动程序的 NDIS [ **MiniportCoDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559356)函数 （请参阅下图）。 *MiniportCoDeactivateVc*与终止的所有通信跨此 VC 其网络适配器进行通信 （例如，清除接收或发送适配器上的缓冲区）。

![说明启动 vc 停用呼叫管理器的关系图](images/cm-08.png)

它将停用 VC 之前，微型端口驱动程序必须完成 VC 上任何挂起的传输。 也就是说，微型端口驱动程序必须等待，直到完成正在进行中的所有发送，直到所有接收已指明数据包将返回到它。 停用 VC 后微型端口驱动程序不能指示接收或传输上 VC 发送。

请注意， *MiniportCoDeactivateVc*不会删除 VC。 创建者 （客户端、 呼叫管理器或 MCM 驱动程序） 的特定 VC 不会重复使用调用[ **NdisCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561698)到[销毁该 VC](deleting-a-vc.md)。 可以为已停用的 VC[重新激活](activating-a-vc.md)通过面向连接的客户端、 调用管理器中或 MCM 驱动程序。

*MiniportCoDeactivateVc*可以同步或异步完成。 调用[ **NdisMCoDeactivateVcComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563559)。 导致要调用的 NDIS [ **ProtocolCmDeactivateVcComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff570242)最初请求 VC 停用的调用管理器的函数。 完成停用意味着激活适用于 VC 的所有调用参数不再有效。 除要将其重新激活了一组新的调用参数禁止 VC 任何进一步使用。

对 MCM 驱动程序调用**NdisMCmDeactivateVc**通知 NDIS，它已停用 VC 或更改已建立 VC 的调用参数 （请参阅下图）。 NDIS 通过调用在 MCM 驱动程序来完成停用序列*ProtocolCmDeactivateVcComplete*函数。

![说明启动 vc 停用的 mcm 驱动程序的关系图](images/fig1-08.png)

MCM 驱动程序不会调用**NdisMCmDeactivateVc**停用 VCs 用于交换 MCM 驱动程序和网络组件，如交换机之间的信号消息。 MCM 驱动程序会停用信号 VC 内部而不会调用任何**Ndis * Xxx*** 函数。

 

 





