---
title: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS 是一个 TLV，其中包含用于通过 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 发送 Wi-fi Direct 操作请求帧的参数。
ms.assetid: 802654D0-CC8E-4808-8C1B-BAAF4C6E53F1
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 394e7f138bfa37e1bb86fad26b8b66e81308088d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845126"
---
# <a name="wdi_tlv_p2p_send_action_request_frame_parameters"></a>WDI\_TLV\_P2P\_发送\_操作\_请求\_帧\_参数


WDI\_TLV\_P2P\_发送\_操作\_请求\_帧\_参数是一个 TLV，其中包含用于通过[OID\_WDI\_任务发送 Wi-fi 直接操作请求帧的参数\_P2P\_发送\_请求\_操作\_帧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame)。

## <a name="tlv-type"></a>TLV 类型


0x8B

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述                                                                                                                    |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_操作\_帧\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 要发送的请求的类型。                                                                                                   |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 目标对等设备的 MAC 地址。                                                                                     |
| UINT8                                                                   | 事务的直接对话框标记。                                                                                   |
| UINT32                                                                  | 发送超时。 发送操作帧的最长时间（以毫秒为单位）。                                                 |
| UINT32                                                                  | 确认后停留时间。 确认传入数据包后在侦听通道上保留的时间（以毫秒为单位）。 |

 

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

 

 




