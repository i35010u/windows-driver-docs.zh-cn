---
title: 面向连接的 NDIS 微型端口驱动程序
description: 面向连接的 NDIS 微型端口驱动程序
ms.assetid: 58f9bed1-274c-4f60-87cd-f0b44871eb60
keywords:
- 微型端口驱动程序 WDK 网络类型
- NDIS 微型端口驱动程序 WDK，类型
- 面向连接的驱动程序 WDK 网络，微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4569bbf10f009e095b8ddf36835f6fc637309f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374967"
---
# <a name="connection-oriented-ndis-miniport-drivers"></a>面向连接的 NDIS 微型端口驱动程序





一个*面向连接的微型端口驱动程序*控制一个或多个面向连接的媒体的微型端口适配器。 面向连接的微型端口驱动程序必须反序列化。 有关反序列化的驱动程序的详细信息，请参阅[反序列化的 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

面向连接的微型端口驱动程序提供了面向连接的协议驱动程序 （面向连接的客户端和调用管理器） 和 NIC 硬件 （例如，物理微型端口适配器） 之间的接口。 通过面向连接的微型端口驱动程序执行的面向连接的操作的摘要，请参阅[Connection-Oriented 微型端口驱动程序执行的操作](connection-oriented-operations-performed-by-miniport-drivers.md)。

面向连接的微型端口驱动程序必须将注册以下*MiniportXxx*函数特定于面向连接的操作：

-   [**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)

-   [**MiniportCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_delete_vc)

-   [**MiniportCoActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_activate_vc)

-   [**MiniportCoDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_deactivate_vc)

-   [**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)

-   [**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)

有关注册这些函数的详细信息，请参阅[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)。

 

 





