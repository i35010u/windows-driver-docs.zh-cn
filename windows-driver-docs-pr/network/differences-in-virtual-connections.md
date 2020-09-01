---
title: 虚拟连接的差异
description: 虚拟连接的差异
ms.assetid: 6e705f31-eec7-4b9c-a46f-ff7641d224c2
keywords:
- 虚拟连接 WDK CoNDIS、MCM 驱动程序与呼叫管理器
- 通知 VCs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52f4be1aa1e038855ffbdafcd2b0e4e13e3748b1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217658"
---
# <a name="differences-in-virtual-connections"></a>虚拟连接的差异





呼叫管理器使用 *信号 VCs* 来发送和接收来自网络实体（例如交换机）的信号消息。 呼叫管理器的信号 VCs 对于 NDIS 可见。 调用管理器必须创建、激活、停用和删除所有 VCs，并调用 NDIS。 然而，MCM driver 的信号 VCs 对于 NDIS 是不透明的。 MCM 驱动程序不会创建、激活、停用和删除使用 NDIS 调用的信号 VCs。 相反，MCM 驱动程序在内部执行此类操作。 MCM 驱动程序必须调用 NDIS，才能在用于发送或接收客户端数据的 VCs 上执行操作。 这是因为 NDIS 必须跟踪客户端 VCs。

因为 MCM 驱动程序既是呼叫管理器又是微型端口驱动程序，所以，某些面向连接的函数是多余的。 具体来说， [**MiniportCoCreateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc) 和 [**MiniportCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc) 是冗余的，因此不由 MCM 驱动程序提供。 VC 操作的处理方式如下：

-   当客户端请求创建或删除 VC 时，MCM 驱动程序的 [**ProtocolCoCreateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc) 和 [**ProtocolCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_delete_vc) 函数。

-   当 MCM 驱动程序创建或删除 VC 时， [**NdisMCmCreateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)和[**NdisMCmDeleteVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc) 。

-   [**NdisMCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc) 和 [**NdisCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) 在 MCM 驱动程序激活或停用 VC 时使用。

MCM 驱动程序必须为客户端提供 [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数，以用于查询或设置微型端口驱动程序信息，并提供 [**MiniportCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists) 函数来处理客户端发送操作。

 

