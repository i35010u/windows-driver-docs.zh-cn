---
title: 协议的 NDIS 驱动程序简介
description: 协议的 NDIS 驱动程序简介
ms.assetid: 398a1cf1-9bf8-45a5-9b6d-65467d061e99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c85109f5611e60fd47575ee30e97b46b208a2874
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524137"
---
# <a name="introduction-to-ndis-protocol-drivers"></a>协议的 NDIS 驱动程序简介


NDIS 协议驱动程序将一组导出*ProtocolXxx*函数在其下边缘。 使用 NDIS 发送和接收网络数据，这样的协议驱动程序进行通信。 协议驱动程序将绑定到基础微型端口驱动程序或中间驱动程序，它将导出*MiniportXxx*接口在其上边缘。

**请注意**  微型端口驱动程序的上边缘中间驱动程序 （虚拟微型端口） 不会管理物理设备。 基础的微型端口驱动程序管理物理设备。

 

协议驱动程序始终使用 NDIS 提供的函数与基础的 NDIS 驱动程序来发送和接收网络数据进行通信。 例如，有一个无连接较低的边缘 （这与无连接媒体，例如以太网基础驱动程序进行通信） 的协议驱动程序必须调用[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)到将网络数据发送到基础的 NDIS 驱动程序。 协议驱动程序可以调用[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710)查询或设置 Oid 的基础无连接驱动程序支持。 有面向连接的下边缘 （这与基础驱动程序对于面向连接的媒体，例如 ISDN） 协议驱动程序必须调用[ **NdisCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561728)发送网络数据复制到较低级别的 NDIS 驱动程序。 它还可以调用[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)查询或设置基础面向连接的驱动程序支持的 Oid。

NDIS 还提供了一套**Ndis * Xxx*** 隐藏基础操作系统的详细信息的函数。 例如，协议驱动程序可以调用[ **NdisInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff562732)若要创建用于同步的事件并[ **NdisInitializeListHead**](https://msdn.microsoft.com/library/windows/hardware/ff562734)创建链接的列表。 使用此类函数的 NDIS 版本的协议驱动程序是在 Microsoft 操作系统更易于移植。 但是，协议驱动程序还可以调用内核模式下支持例程，如[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)。 有关详细信息，请参阅[内核模式下支持例程的摘要](https://msdn.microsoft.com/library/windows/hardware/ff563889)。

协议驱动程序的开发人员应使用相同[的编程注意事项](network-driver-programming-considerations.md)由应用于其他的 NDIS 驱动程序。

 

 





