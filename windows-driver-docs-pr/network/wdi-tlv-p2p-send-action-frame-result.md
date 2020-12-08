---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT 是一种 TLV，其中包含有关发送到对等方的操作帧的信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2cf90bd78673ec9bb22ea904ab9b432b520c2045
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818141"
---
# <a name="wdi_tlv_p2p_send_action_frame_result"></a>WDI \_ TLV \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果


WDI \_ tlv \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果是一个 TLV，其中包含有关发送到对等方的操作帧的信息。

## <a name="tlv-type"></a>TLV 类型


0xAF

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                              | 允许多个 TLV 实例 | 可选 | 说明                                           |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 发送 \_ 操作 \_ 帧 \_ 结果 \_ 参数**](wdi-tlv-p2p-send-action-frame-result-parameters.md) |                                |          | Wi-Fi 直接发送操作帧结果参数。 |
| [**WDI \_ TLV \_ P2P \_ 操作 \_ 帧 \_**](wdi-tlv-p2p-action-frame-ies.md)                                         |                                |          | 发送到远程设备的一组。             |

 

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

 

 




