---
title: NDIS 协议驱动程序简介
description: NDIS 协议驱动程序简介
ms.assetid: 398a1cf1-9bf8-45a5-9b6d-65467d061e99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2deccc9dfccbb36ad7120146d009ea1e1c50f317
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844162"
---
# <a name="introduction-to-ndis-protocol-drivers"></a>NDIS 协议驱动程序简介


NDIS 协议驱动程序在其下边缘导出一组*ProtocolXxx*函数。 此类协议驱动程序与 NDIS 通信以发送和接收网络数据。 协议驱动程序绑定到基础微型端口驱动程序或中间驱动程序，用于在其上边缘导出*MiniportXxx*接口。

**请注意**  ，中间驱动程序的小型小型驱动程序（虚拟微型端口）的上边缘不管理物理设备。 底层微型端口驱动程序管理物理设备。

 

协议驱动程序始终使用 NDIS 提供的函数来与基础 NDIS 驱动程序通信，以便发送和接收网络数据。 例如，如果某个协议驱动程序具有不连接的下层边缘（与无连接媒体（如以太网）的底层驱动程序通信），则必须调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists) ，将网络数据发送到基础 NDIS 驱动程序。 协议驱动程序可以调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)来查询或设置基础无连接驱动程序支持的 oid。 如果协议驱动程序具有面向连接的下边缘（与面向连接的媒体（如 ISDN）的基础驱动程序通信），则必须调用[**NdisCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscosendnetbufferlists) ，将网络数据发送到较低级别的 NDIS 驱动程序。 它还可以调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)来查询或设置面向基础连接的驱动程序所支持的 oid。

NDIS 还提供了一组用于隐藏基础操作系统详细信息的**Ndis<em>Xxx</em>** 函数。 例如，协议驱动程序可以调用[**NdisInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeevent)来创建用于同步目的的事件，并使用[**NdisInitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializelisthead)创建链接列表。 使用此类函数的 NDIS 版本的协议驱动程序在 Microsoft 操作系统中更易于移植。 但协议驱动程序还可以调用内核模式支持例程，如[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)。 有关详细信息，请参阅[内核模式支持例程摘要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

协议驱动程序的开发人员应使用适用于其他 NDIS 驱动程序的相同[编程注意事项](network-driver-programming-considerations.md)。

 

 





