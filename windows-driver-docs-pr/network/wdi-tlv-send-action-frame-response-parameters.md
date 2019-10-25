---
title: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS 是一个 TLV，其中包含 OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME 的参数。
ms.assetid: F062F8A2-EEEF-4EFC-AEC8-F1D7AB13C899
ms.date: 07/18/2017
keywords:
- WDI_TLV_SEND_ACTION_FRAME_RESPONSE_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2319c333a501dc34ef8678d942470a3bd38c6a4f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841733"
---
# <a name="wdi_tlv_send_action_frame_response_parameters"></a>WDI\_TLV\_发送\_操作\_帧\_响应\_参数


WDI\_TLV\_发送\_操作\_帧\_的参数是一个 TLV，其中包含 OID 的参数[\_WDI\_\_\_\_\_\_帧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-send-response-action-frame)。

## <a name="tlv-type"></a>TLV 类型


0xE2

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                              | 描述                                                                                                                                     |
|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WDI\_通道\_号（UINT32）                     | 要将操作帧发送到的通道，还会按确认后停留时间中指定的频率进行逗留。                                    |
| WDI\_波段\_ID （UINT32）                            | 要在其上发送操作帧的带区的 ID。                                                                                           |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 目标访问点或对等适配器的 MAC 地址。                                                                                     |
| UINT32                                            | 发送超时。 指定发送此操作帧的最长时间（毫秒）。                                                       |
| UINT32                                            | 确认后停留时间。 指定在确认传入数据包后，要在侦听通道上保留的时间（以毫秒为单位）。 |

 

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
<td><p>Windows 10</p></td>
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

 

 




