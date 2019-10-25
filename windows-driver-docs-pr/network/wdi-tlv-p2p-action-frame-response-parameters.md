---
title: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS 是包含 Wi-fi Direct 操作帧响应参数的 TLV。
ms.assetid: 2DFF00A6-FDE2-43EF-93C2-EEA3DBC00D52
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 90d026eac9fa442263baff118ff42537f7247f30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824351"
---
# <a name="wdi_tlv_p2p_action_frame_response_parameters"></a>WDI\_TLV\_P2P\_操作\_帧\_响应\_参数


WDI\_TLV\_P2P\_操作\_帧\_响应\_参数是包含 Wi-fi Direct 操作帧响应参数的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xAD

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述                                                                                                                          |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_操作\_帧\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 要发送的响应帧的类型。                                                                                               |
| [**WDI\_MAC\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 目标对等 Wi-fi Direct 设备的设备地址。                                                                           |
| UINT8                                                                   | 此事务的 Wi-fi Direct 对话框令牌。                                                                                  |
| UINT32                                                                  | 发送超时。 指定发送此操作帧的最长时间（以毫秒为单位）。                                            |
| UINT32                                                                  | 确认后停留时间。 指定在确认传入数据包后，在侦听通道上保留的时间（以毫秒为单位）。 |

 

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

 

 




