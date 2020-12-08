---
title: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS
description: WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS 是包含传入 Wi-Fi 直接操作帧参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INCOMING_FRAME_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 405d66172dfd1130520d979fe6f8f5de05a21ef8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818246"
---
# <a name="wdi_tlv_p2p_incoming_frame_parameters"></a>WDI \_ TLV \_ P2P \_ 传入 \_ 帧 \_ 参数


WDI \_ tlv \_ P2P \_ 传入 \_ 帧 \_ 参数是包含传入 Wi-Fi 直接操作帧参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x7A

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                    | 描述                                        |
|-------------------------------------------------------------------------|----------------------------------------------------|
| [**WDI \_ P2P \_ 操作 \_ 帧 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 传入操作帧的类型。             |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 远程对等方的 MAC 地址。                |
| UINT8                                                                   | 事务的 Wi-Fi 直接对话框标记。 |

 

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

 

