---
title: 将 GUID 映射到 OID 和微型端口驱动程序状态
description: 将 GUID 映射到 OID 和微型端口驱动程序状态
ms.assetid: b3c9bb40-2906-4059-b9fa-06f6ababd3f2
keywords:
- WMI WDK 网络，Guid
- Oid WDK 网络，WMI
- Guid WDK 网络
- Windows Management Instrumentation WDK 网络，Guid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 713984abb5d52e56321c3d55e1c3b420ca0df9c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844306"
---
# <a name="mapping-of-guids-to-oids-and-miniport-driver-status"></a>将 GUID 映射到 OID 和微型端口驱动程序状态





当 WMI 向微型端口适配器发送 WMI 请求时（即，当 WMI 将 i/o 请求数据包 \[IRP\] 发送到 NDIS 创建的功能设备对象时，NDIS 会截获该请求。 如果 NDIS 已经包含为请求提供服务所需的信息，NDIS 不会将请求转发到微型端口驱动程序。 否则，NDIS 会将 WMI GUID 映射到 OID，然后查询或设置 OID。

如果微型端口驱动程序是无连接微型端口驱动程序，NDIS 可以调用微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数来处理 OID 请求。 如果微型端口驱动程序是面向连接的微型端口驱动程序，NDIS 可以调用微型端口驱动程序的[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数来处理 OID 请求。 NDIS 返回查询的结果或将请求设置为 WMI。

微型端口驱动程序通过[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)或[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)函数生成状态指示。 如果 WMI 客户端注册 WMI 事件，而微型端口驱动程序生成关联的状态指示，NDIS 会将该状态指示映射到 WMI GUID，并将 WMI 事件指示传递到 WMI。 WMI 随后会将 WMI 事件指示传递到已为 WMI 事件注册的所有 WMI 客户端。

 

 





