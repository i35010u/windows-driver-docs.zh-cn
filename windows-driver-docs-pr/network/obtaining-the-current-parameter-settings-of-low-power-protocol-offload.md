---
title: 获取低功耗协议卸载的当前参数设置
description: 获取低功耗协议卸载的当前参数设置
ms.assetid: 53d8535f-0615-4ba2-92f4-1c20a7d12c8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d3189321632cfd7cb72d5cf6d01e5a507c07951
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354512"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>获取低功耗协议卸载的当前参数设置





协议驱动程序可以使用[OID\_PM\_协议\_卸载\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)OID 查询以获取所有已卸载的网络适配器上该协议的协议的列表。 从查询中，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含指针到一系列[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)描述当前处于活动状态的协议的结构将卸载。 有关的内容信息**NDIS\_PM\_协议\_卸载**结构，请参阅[添加和删除低电源协议卸载](adding-and-deleting-low-power-protocol-offloads.md)。

NDIS 句柄[OID\_PM\_协议\_卸载\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)OID 和 GUID\_PM\_协议\_卸载\_列表 WMI代表微型端口驱动程序的请求。 因此，NDIS 微型端口驱动程序不支持所需 OID\_PM\_协议\_卸载\_列表 OID 请求。

过量驱动程序可以使用[OID\_PM\_获取\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-get-protocol-offload)方法要获取的低能耗协议参数设置的 OID 将卸载从微型端口驱动程序。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构最初包含一个指向协议卸载标识符。 从方法请求成功返回后**InformationBuffer**的成员**NDIS\_OID\_请求**结构包含一个指向[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构。

 

 





