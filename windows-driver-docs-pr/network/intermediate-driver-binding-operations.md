---
title: 中间驱动程序绑定操作
description: 中间驱动程序绑定操作
ms.assetid: 129a744c-d4d4-4741-9812-e76087c585fc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 468ea83f8f68cca1f51d2ef8796fdc82878a58d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844188"
---
# <a name="intermediate-driver-binding-operations"></a>中间驱动程序绑定操作





当微型端口适配器可用时，NDIS 将调用可以绑定到该微型端口适配器的任何中间驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数。

中间驱动程序必须提供[绑定到适配器时](binding-to-an-adapter.md)所记录的协议绑定操作。

绑定时操作包括为绑定分配和初始化适配器特定的上下文区域，初始化任何虚拟微型端口，以及调用[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)以绑定到适配器。

中间驱动程序不需要为每个绑定分配单独的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构池。 仅当驱动程序设计要求它分配其自己的结构时，才需要中间驱动程序才能将 NET\_BUFFER\_列表结构池分配。 否则，驱动程序可以只传递从其他驱动程序接收的结构。 此类驱动程序应为发送和接收分配不同的池。

有关分配和管理网络数据的要求的信息，请参阅[中间驱动程序网络数据管理](intermediate-driver-network-data-management.md)。

 

 





