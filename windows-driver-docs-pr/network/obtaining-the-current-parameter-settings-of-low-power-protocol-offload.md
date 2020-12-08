---
title: 获取低功耗协议卸载的当前参数设置
description: 获取低功耗协议卸载的当前参数设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b595daabad631eea6415981896e4ddb310c3c73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832159"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>获取低功耗协议卸载的当前参数设置





协议驱动程序可以使用 [oid \_ PM \_ 协议 \_ 卸载 \_ 列表](./oid-pm-protocol-offload-list.md) OID 查询获取网络适配器上该协议已卸载的所有协议的列表。 成功从查询返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含一个指针，该指针指向描述当前活动的协议 [**卸载的 NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的列表。 有关 **NDIS \_ PM \_ 协议 \_ 卸载** 结构的内容的信息，请参阅 [添加和删除低能耗协议](adding-and-deleting-low-power-protocol-offloads.md)卸载。

NDIS 处理 [OID \_ pm \_ 协议 \_ 卸载 \_ 列表](./oid-pm-protocol-offload-list.md) oid 和 GUID \_ pm \_ 协议 \_ 卸载 \_ 列出了代表微型端口驱动程序的 WMI 请求。 因此，不需要 NDIS 微型端口驱动程序来支持 OID \_ PM \_ 协议 \_ 卸载 \_ 列表 oid 请求。

过量驱动程序可以使用 [oid \_ PM \_ 获取 \_ 协议 \_ 卸载](./oid-pm-get-protocol-offload.md) 方法 OID，从微型端口驱动程序中获取用于低功率协议卸载的参数设置。 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员最初包含指向协议卸载标识符的指针。 成功从方法请求返回后， **ndis \_ OID \_ 请求** 结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

 

