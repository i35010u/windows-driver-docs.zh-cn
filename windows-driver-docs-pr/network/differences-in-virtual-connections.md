---
title: 虚拟连接的差异
description: 虚拟连接的差异
ms.assetid: 6e705f31-eec7-4b9c-a46f-ff7641d224c2
keywords:
- 虚拟连接 WDK 的 CoNDIS，与 MCM 驱动程序调用管理器
- 信号 VCs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b613b84fc7355297d9e91bb7c946a6c6c34a0c2a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381377"
---
# <a name="differences-in-virtual-connections"></a>虚拟连接的差异





呼叫管理器使用*信号 VCs*发送和接收网络实体，如交换机的信号消息。 调用管理器的信号 VCs 是到 NDIS 可见的。 呼叫管理器必须创建、 激活、 停用，并删除所有与调用到 NDIS VCs。 MCM 驱动程序的信号 VCs，但是，是不透明的 NDIS。 MCM 驱动程序不会不创建、 激活、 停用，和删除信号 VCs NDIS 调用。 相反，MCM 驱动程序将在内部执行此类操作。 MCM 驱动程序必须调用 NDIS VCs 用来发送或接收客户端数据上执行操作。 这是因为 NDIS 必须跟踪的客户端 VCs。

由于 MCM 驱动程序呼叫管理器和微型端口驱动程序，某些面向连接的函数是冗余的。 具体而言， [ **MiniportCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)并[ **MiniportCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_delete_vc)冗余，因此未提供的 MCM 驱动程序。 VC 操作由处理：

-   MCM 驱动程序[ **ProtocolCoCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_create_vc)并[ **ProtocolCoDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_delete_vc)函数时客户端请求创建或删除VC。

-   [**NdisMCmCreateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmcreatevc)并[ **NdisMCmDeleteVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmdeletevc) MCM 驱动程序时创建或删除 VC。

-   [**NdisMCmActivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmactivatevc)并[ **NdisCmDeactivateVc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmdeactivatevc) MCM 驱动程序当激活或停用 VC。

MCM 驱动程序必须提供[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)客户端可以在查询或设置微型端口驱动程序信息中使用的函数和一个[ **MiniportCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数以处理从客户端发送操作。

 

 





