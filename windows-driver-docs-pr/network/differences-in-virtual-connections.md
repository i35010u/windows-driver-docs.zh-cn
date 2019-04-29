---
title: 虚拟连接的差异
description: 虚拟连接的差异
ms.assetid: 6e705f31-eec7-4b9c-a46f-ff7641d224c2
keywords:
- 虚拟连接 WDK 的 CoNDIS，与 MCM 驱动程序调用管理器
- 信号 VCs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bda82d768f2e8c008e5dd677e67d705cbd4e57ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379573"
---
# <a name="differences-in-virtual-connections"></a>虚拟连接的差异





呼叫管理器使用*信号 VCs*发送和接收网络实体，如交换机的信号消息。 调用管理器的信号 VCs 是到 NDIS 可见的。 呼叫管理器必须创建、 激活、 停用，并删除所有与调用到 NDIS VCs。 MCM 驱动程序的信号 VCs，但是，是不透明的 NDIS。 MCM 驱动程序不会不创建、 激活、 停用，和删除信号 VCs NDIS 调用。 相反，MCM 驱动程序将在内部执行此类操作。 MCM 驱动程序必须调用 NDIS VCs 用来发送或接收客户端数据上执行操作。 这是因为 NDIS 必须跟踪的客户端 VCs。

由于 MCM 驱动程序呼叫管理器和微型端口驱动程序，某些面向连接的函数是冗余的。 具体而言， [ **MiniportCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559354)并[ **MiniportCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559358)冗余，因此未提供的 MCM 驱动程序。 VC 操作由处理：

-   MCM 驱动程序[ **ProtocolCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570252)并[ **ProtocolCoDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570253)函数时客户端请求创建或删除VC。

-   [**NdisMCmCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562812)并[ **NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819) MCM 驱动程序时创建或删除 VC。

-   [**NdisMCmActivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562792)并[ **NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657) MCM 驱动程序当激活或停用 VC。

MCM 驱动程序必须提供[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)客户端可以在查询或设置微型端口驱动程序信息中使用的函数和一个[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)函数以处理从客户端发送操作。

 

 





