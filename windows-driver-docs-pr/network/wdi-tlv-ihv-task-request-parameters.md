---
title: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS
description: WDI_TLV_IHV_TASK_REQUEST_PARAMETERS 是包含 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST 请求优先级的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_TASK_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bf5b9143f169d4d7b24b7c59b0428818dd391319
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791285"
---
# <a name="wdi_tlv_ihv_task_request_parameters"></a>WDI \_ TLV \_ IHV \_ 任务 \_ 请求 \_ 参数


WDI \_ tlv \_ IHV \_ 任务 \_ 请求 \_ 参数是一个 tlv，其中包含 [NDIS \_ STATUS \_ WDI \_ 指示 \_ IHV \_ 任务 \_ 请求](./ndis-status-wdi-indication-ihv-task-request.md)的请求优先级。

## <a name="tlv-type"></a>TLV 类型


0xDF

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                             |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | IHV 请求此任务的优先级。 有关有效的优先级值，请参阅 [**WDI \_ IHV \_ 任务 \_ 优先级**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ihv_task_priority) 。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

