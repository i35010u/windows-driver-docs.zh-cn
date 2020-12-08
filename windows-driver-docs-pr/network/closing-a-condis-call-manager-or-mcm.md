---
title: 关闭 CoNDIS 呼叫管理程序或 MCM
description: 关闭 CoNDIS 呼叫管理程序或 MCM
keywords:
- 呼叫经理 WDK 网络，CoNDIS
- MCMs WDK 网络，关闭
- 微型端口呼叫管理器 WDK 网络，关闭
- 关闭呼叫管理器
- 关闭微型端口调用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92db9c337ec95ed5dadb6f436abd13f6c2f378c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832633"
---
# <a name="closing-a-condis-call-manager-or-mcm"></a>关闭 CoNDIS 呼叫管理程序或 MCM





当独立呼叫管理器从基础微型端口适配器取消绑定时，呼叫管理器必须通知受影响的所有 CoNDIS 客户端必须关闭关联的 AF。 为了通知每个客户端，NDIS 独立调用管理器调用 [**NdisCmNotifyCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily) 函数。

如果 MCM 管理的 CoNDIS 微型端口适配器正在停止，则 MCM 必须通知所有受影响的客户端必须关闭关联的 AF。 为了通知每个客户端，MCMs 将调用 [**NdisMCmNotifyCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmnotifycloseaddressfamily) 函数。

如果独立调用管理器或 MCM 分别调用 **NdisCmNotifyCloseAddressFamily** 或 **NdisMCmNotifyCloseAddressFamily**，NDIS 将调用与 **CoNDIS 或** **NdisAfHandle** 的 *NdisCmNotifyCloseAddressFamily* 参数中的句柄关联的 NdisMCmNotifyCloseAddressFamily 客户端的 [**ProtocolClNotifyCloseAf**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_notify_close_af)函数。 此调用会通知客户端关闭 AF。 如果 **NdisCmNotifyCloseAddressFamily** 或 **NdisMCmNotifyCloseAddressFamily** 返回 NDIS \_ 状态 \_ 挂起，则在关闭通知操作完成后，NDIS 将调用调用管理器的 [**ProtocolCmNotifyCloseAfComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_notify_close_af_complete) 函数。

有关在 CoNDIS 客户端中关闭地址族的详细信息，请参阅 [在 CoNDIS 客户端中关闭地址族](closing-an-address-family-in-a-condis-client.md)。

 

