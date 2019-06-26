---
title: 报告 NIC 的 IPsec 卸载版本 2 功能
description: 报告 NIC 的 IPsec 卸载版本 2 功能
ms.assetid: 0ce5c42d-5c0c-4dfa-8a9f-a80c8924201d
keywords:
- IPsecOV2 WDK TCP/IP 传输功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab959b80e4a03c609f8c19e6cf3cfceac2ec14b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373283"
---
# <a name="reporting-a-nics-ipsec-offload-version-2-capabilities"></a>报告 NIC 的 IPsec 卸载版本 2 功能

\[IPsec 任务卸载功能已弃用，不应使用。\]




若要指定 IPsec 卸载版本 2 (IPsecOV2) 功能、 NDIS 6.1 和更高版本的微型端口驱动程序指定当前或默认配置中的 nic [ **NDIS\_IPSEC\_卸载\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构。 微型端口驱动程序必须包括中的默认 IPsecOV2 配置[ **NDIS\_微型端口\_适配器\_卸载\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数从[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数并传递中信息在 NDIS\_微型端口\_适配器\_卸载\_属性。

微型端口驱动程序必须报告 IPsecOV2 功能中的更改，如果有，请在[ **NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示。

**请注意**  NDIS NDIS 6.1 和更高版本的驱动程序提供直接的 OID 请求接口。 [直接 OID 请求路径](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)支持查询或频繁设置的 OID 请求。

 

中的查询响应[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，NDIS 包括 NDIS\_IPSEC\_卸载\_V2结构中[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS 返回中的结构**InformationBuffer**隶属[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 NDIS 使用微型端口驱动程序提供的信息。

 

 





