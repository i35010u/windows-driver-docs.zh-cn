---
title: 将 GUID 映射到 OID 和微型端口驱动程序状态
description: 将 GUID 映射到 OID 和微型端口驱动程序状态
ms.assetid: b3c9bb40-2906-4059-b9fa-06f6ababd3f2
keywords:
- WMI WDK 网络、 Guid
- Oid WDK 网络 WMI
- Guid WDK 网络
- Windows Management Instrumentation WDK 网络 Guid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97fd94e974bb0aa0021130997690b7531bdb2349
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369171"
---
# <a name="mapping-of-guids-to-oids-and-miniport-driver-status"></a>将 GUID 映射到 OID 和微型端口驱动程序状态





WMI 将 WMI 请求中发送到的微型端口适配器 (即，当 WMI 发送的 I/O 请求数据包\[IRP\]到 NDIS 创建功能的设备对象)，NDIS 截获的请求。 NDIS 不转发对微型端口驱动程序的请求，如果 NDIS 已有，它需要要为请求提供服务的信息。 否则为 NDIS WMI GUID 映射到 OID，然后查询或设置 OID。

NDIS 如果微型端口驱动程序是一个无连接的微型端口驱动程序，可以调用微型端口驱动程序[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数以处理 OID 请求。 NDIS 如果微型端口驱动程序是一个面向连接的微型端口驱动程序，可以调用微型端口驱动程序[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)函数以处理 OID 请求。 NDIS 返回查询的结果或与 WMI 的集请求。

微型端口驱动程序生成的状态指示[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)或[ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)函数。 如果 WMI 客户端注册 WMI 事件和微型端口驱动程序将生成的关联的状态指示，NDIS 将该状态指示映射到 WMI GUID，并将 WMI 事件指示传递到 WMI。 然后，WMI 将 WMI 事件指示传递给所有已注册的 WMI 事件的 WMI 客户端。

 

 





