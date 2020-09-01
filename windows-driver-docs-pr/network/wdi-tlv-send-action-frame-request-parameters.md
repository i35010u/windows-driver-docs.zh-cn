---
title: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS 是包含 OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME 的参数的 TLV。
ms.assetid: 92629752-A94B-442A-97E9-D8E1C7924855
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SEND_ACTION_FRAME_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ec3bccfcf3652841ab754b58b5bf96a108f60333
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207745"
---
# <a name="wdi_tlv_send_action_frame_request_parameters"></a>WDI \_ TLV \_ 发送 \_ 操作 \_ 帧 \_ 请求 \_ 参数


WDI \_ tlv \_ 发送 \_ 操作 \_ 帧 \_ 请求 \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ TASK \_ 发送 \_ 请求 \_ 操作 \_ 帧](./oid-wdi-task-send-request-action-frame.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0xBF

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 说明                                                                                                                                     |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WDI \_ 信道 \_ 号 (UINT32)                      | 要将操作帧发送到的通道，还会按确认后停留时间中指定的频率进行逗留。                                    |
| WDI \_ 波段 \_ ID (UINT32)                             | 要在其上发送操作帧的带区的 ID。                                                                                           |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目标访问点或对等适配器的 MAC 地址。                                                                                     |
| UINT32                                            | 发送超时。 指定发送此操作帧)  (的最长时间（以毫秒为单位）。                                                       |
| UINT32                                            | 确认后停留时间。 指定在确认传入数据包后) 在侦听通道上保留的时间（以毫秒为单位） (。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

