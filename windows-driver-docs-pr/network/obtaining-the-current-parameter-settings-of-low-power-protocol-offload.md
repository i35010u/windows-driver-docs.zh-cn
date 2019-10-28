---
title: 获取低功耗协议卸载的当前参数设置
description: 获取低功耗协议卸载的当前参数设置
ms.assetid: 53d8535f-0615-4ba2-92f4-1c20a7d12c8d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc19bed34980a8f615743f13771ed28a5dfcb1a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837742"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>获取低功耗协议卸载的当前参数设置





协议驱动程序可以使用[OID\_PM\_协议\_卸载\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)OID 查询，以获取网络适配器上该协议已卸载的所有协议的列表。 成功从查询返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个指向 ndis\_PM 的列表的指针[ **\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构，描述当前处于活动状态的协议卸载。 有关 NDIS\_PM 的内容的信息 **\_协议\_卸载**结构，请参阅[添加和删除低能耗协议卸载](adding-and-deleting-low-power-protocol-offloads.md)。

NDIS 处理[OID\_pm\_协议\_卸载\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-protocol-offload-list)OID 和 GUID\_PM\_协议\_卸载\_代表微型端口驱动程序列出 WMI 请求。 因此，不需要 NDIS 微型端口驱动程序支持 OID\_PM\_协议\_卸载\_列表 OID 请求。

过量驱动程序可以使用[OID\_PM\_获取\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-get-protocol-offload)方法 OID，以获取来自微型端口驱动程序的低功率协议卸载的参数设置。 [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员最初包含指向协议卸载标识符的指针。 成功从方法请求返回后， **ndis\_OID\_请求**结构的**InformationBuffer**成员包含指向[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

 

 





