---
title: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
description: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
ms.assetid: 6EBC0131-F2EF-4A2D-997A-8990E53369CF
ms.date: 02/11/2019
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 90d173cbabb928e587cadf16c2f8c92855748059
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905327"
---
# <a name="ndisstatuswdiindicationrequestftmcomplete"></a>NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE

微型端口驱动程序发送**NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE**到主机的任务完成指示的状态指示[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)。 此通知包含正常计时度量 (FTM) 从收到的响应每个请求的目标列表。

## <a name="payload-data"></a>有效负载数据

| 在任务栏的搜索框中键入 | TLV | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- |--- | --- | --- |
| WDI_STATUS | 标头中的字段。  |   | 事件的常规的完成状态。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | Multiple TLV\<WDI_TLV_FTM_RESPONSE> | X |   | 为每个目标的 FTM 响应的列表。 |

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| 最低受支持的客户端 | Windows 10，版本 1903 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Dot11wdi.h |
