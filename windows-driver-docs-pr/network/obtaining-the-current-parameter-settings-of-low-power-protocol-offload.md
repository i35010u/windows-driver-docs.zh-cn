---
title: 获取低功耗协议卸载的当前参数设置
description: 获取低功耗协议卸载的当前参数设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4519fdf0541f14a15d51d0044bbeba3cb6199ec8
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248407"
---
# <a name="obtaining-the-current-parameter-settings-of-low-power-protocol-offloads"></a>获取低功耗协议卸载的当前参数设置





协议驱动程序可以使用 [oid \_ PM \_ 协议 \_ 卸载 \_ 列表](./oid-pm-protocol-offload-list.md) OID 查询获取网络适配器上该协议已卸载的所有协议的列表。 成功从查询返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含一个指针，该指针指向描述当前活动的协议 [**卸载的 NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的列表。 有关 **NDIS \_ PM \_ 协议 \_ 卸载** 结构的内容的信息，请参阅 [添加和删除低能耗协议](adding-and-deleting-low-power-protocol-offloads.md)卸载。

NDIS 处理 [OID \_ pm \_ 协议 \_ 卸载 \_ 列表](./oid-pm-protocol-offload-list.md) oid 和 GUID \_ pm \_ 协议 \_ 卸载 \_ 列出了代表微型端口驱动程序的 WMI 请求。 因此，不需要 NDIS 微型端口驱动程序来支持 OID \_ PM \_ 协议 \_ 卸载 \_ 列表 oid 请求。

过量驱动程序可以使用 [oid \_ PM \_ 获取 \_ 协议 \_ 卸载](./oid-pm-get-protocol-offload.md) 方法 OID，从微型端口驱动程序中获取用于低功率协议卸载的参数设置。 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员最初包含指向协议卸载标识符的指针。 成功从方法请求返回后， **ndis \_ OID \_ 请求** 结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

 

