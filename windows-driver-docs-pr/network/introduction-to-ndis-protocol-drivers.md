---
title: NDIS 协议驱动程序简介
description: NDIS 协议驱动程序简介
ms.assetid: 398a1cf1-9bf8-45a5-9b6d-65467d061e99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da805bf6e71f3c304b47a0522f72a1aa162586b1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212181"
---
# <a name="introduction-to-ndis-protocol-drivers"></a>NDIS 协议驱动程序简介


NDIS 协议驱动程序在其下边缘导出一组 *ProtocolXxx* 函数。 此类协议驱动程序与 NDIS 通信以发送和接收网络数据。 协议驱动程序绑定到基础微型端口驱动程序或中间驱动程序，用于在其上边缘导出 *MiniportXxx* 接口。

**注意**   中间驱动程序的小型端口驱动程序的上边缘 (虚拟微型端口) 不管理物理设备。 底层微型端口驱动程序管理物理设备。

 

协议驱动程序始终使用 NDIS 提供的函数来与基础 NDIS 驱动程序通信，以便发送和接收网络数据。 例如，有一个协议驱动程序，该驱动程序具有不连接的底层 (，该驱动程序与用于无连接媒体的底层驱动程序通信，如以太网) 必须调用 [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists) ，将网络数据发送到基础 NDIS 驱动程序。 协议驱动程序可以调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 来查询或设置基础无连接驱动程序支持的 oid。 一个协议驱动程序，具有面向连接的下边缘 (与面向连接的媒体（如 ISDN) ）的基础驱动程序通信的协议驱动程序必须调用 [**NdisCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists) ，以便将网络数据发送到更低级别的 NDIS 驱动程序。 它还可以调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 来查询或设置面向基础连接的驱动程序所支持的 oid。

NDIS 还提供了一组用于隐藏基础操作系统详细信息的**Ndis<em>Xxx</em> **函数。 例如，协议驱动程序可以调用 [**NdisInitializeEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeevent) 来创建用于同步目的的事件，并使用 [**NdisInitializeListHead**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializelisthead) 创建链接列表。 使用此类函数的 NDIS 版本的协议驱动程序在 Microsoft 操作系统中更易于移植。 但协议驱动程序还可以调用内核模式支持例程，如 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)。 有关详细信息，请参阅 [内核模式支持例程摘要](/windows-hardware/drivers/ddi/index)。

协议驱动程序的开发人员应使用适用于其他 NDIS 驱动程序的相同 [编程注意事项](network-driver-programming-considerations.md) 。

 

