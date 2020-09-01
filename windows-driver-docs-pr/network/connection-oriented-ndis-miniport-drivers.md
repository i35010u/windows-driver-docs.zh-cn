---
title: 面向连接的 NDIS 微型端口驱动程序
description: 面向连接的 NDIS 微型端口驱动程序
ms.assetid: 58f9bed1-274c-4f60-87cd-f0b44871eb60
keywords:
- 微型端口驱动程序 WDK 网络，类型
- NDIS 微型端口驱动程序 WDK，类型
- 面向连接的驱动程序 WDK 网络，微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e840a0c9095bcc889d73e9b92a7118bb620f4ce5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206469"
---
# <a name="connection-oriented-ndis-miniport-drivers"></a>面向连接的 NDIS 微型端口驱动程序





*面向连接的微型端口驱动程序*控制面向连接的媒体的一个或多个微型端口适配器。 面向连接的微型端口驱动程序必须进行反序列化。 有关反序列化驱动程序的详细信息，请参阅 [反序列化 NDIS 微型端口驱动程序](deserialized-ndis-miniport-drivers.md)。

面向连接的微型端口驱动程序在面向连接的客户端和调用管理器) 和 NIC 硬件 (（例如，物理微型端口适配器) ）之间提供面向连接的协议驱动 (程序之间的接口。 有关面向连接的微型端口驱动程序执行的面向连接的操作的摘要，请参阅 [小型端口驱动程序执行的面向连接的操作](connection-oriented-operations-performed-by-miniport-drivers.md)。

面向连接的微型端口驱动程序必须注册以下特定于面向连接的操作的 *MiniportXxx* 函数：

-   [**MiniportCoCreateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)

-   [**MiniportCoDeleteVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc)

-   [**MiniportCoActivateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_activate_vc)

-   [**MiniportCoDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_deactivate_vc)

-   [**MiniportCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)

-   [**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)

有关注册这些函数的详细信息，请参阅 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)。

 

