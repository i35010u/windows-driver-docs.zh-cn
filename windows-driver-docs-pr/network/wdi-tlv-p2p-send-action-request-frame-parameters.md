---
title: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS 是 TLV，其中包含用于发送与 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME Wi-Fi Direct 操作请求帧的参数。
ms.assetid: 802654D0-CC8E-4808-8C1B-BAAF4C6E53F1
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 32fdbe11f8d4b10d0b6ebeac4d59018fd5044150
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355432"
---
# <a name="wditlvp2psendactionrequestframeparameters"></a>WDI\_TLV\_P2P\_SEND\_ACTION\_REQUEST\_FRAME\_PARAMETERS


WDI\_TLV\_P2P\_发送\_操作\_请求\_帧\_参数是包含参数用于发送与Wi-FiDirect操作请求帧TLV[OID\_WDI\_任务\_P2P\_发送\_请求\_操作\_帧](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame)。

## <a name="tlv-type"></a>TLV 类型


0x8B

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述                                                                                                                    |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_ACTION\_FRAME\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 要发送的请求类型。                                                                                                   |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 目标对等设备的 MAC 地址。                                                                                     |
| UINT8                                                                   | 直接对话框中的标记的事务。                                                                                   |
| UINT32                                                                  | 发送超时。 最长的时间，以毫秒为单位，将发送操作帧。                                                 |
| UINT32                                                                  | 开机自检 ACK 停留时间。 时间，以毫秒为单位，传入的数据包被确认后仍保留在侦听通道上。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




