---
title: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
description: NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE
ms.assetid: 6EBC0131-F2EF-4A2D-997A-8990E53369CF
ms.date: 02/11/2019
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0a6a44f2da4ee51cabb722e442f7b24a86c1a6a1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968316"
---
# <a name="ndis_status_wdi_indication_request_ftm_complete"></a>NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE

小型端口驱动程序将**NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE**状态指示发送到主机，作为[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)的任务完成指示。 此通知包含从每个请求的目标接收的精细计时度量（INTERNAL.H）响应列表。

## <a name="payload-data"></a>负载数据

| 类型 | TLV | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- |--- | --- | --- |
| WDI_STATUS | 标头中的字段。  |   | 事件的一般完成状态。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | 多个 TLV\<WDI_TLV_FTM_RESPONSE> | X |   | 每个目标的 INTERNAL.H 响应列表。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1903

**支持的最低服务器**： Windows server 2016

**标头**： Dot11wdi

