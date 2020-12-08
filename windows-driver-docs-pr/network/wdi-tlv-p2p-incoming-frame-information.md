---
title: WDI_TLV_P2P_INCOMING_FRAME_INFORMATION
description: WDI_TLV_P2P_INCOMING_FRAME_INFORMATION 是包含传入 Wi-Fi 直接操作帧信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INCOMING_FRAME_INFORMATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 30068efdcabd87ad2eb09db62d72ea7e68814ba7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818249"
---
# <a name="wdi_tlv_p2p_incoming_frame_information"></a>WDI \_ TLV \_ P2P \_ 传入 \_ 帧 \_ 信息


WDI \_ tlv \_ P2P \_ 传入 \_ 帧 \_ 信息是包含传入 Wi-Fi 直接操作帧信息的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x79

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                        | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 传入 \_ 帧 \_ 参数**](wdi-tlv-p2p-incoming-frame-parameters.md) |                                |          | 指定传入帧参数。                                                                                                                                                                                        |
| [**WDI \_ TLV \_ P2P \_ 操作 \_ 帧 \_**](wdi-tlv-p2p-action-frame-ies.md)                   |                                |          | 指定收到的公共操作帧的 "中" 部分。                                                                                                                                                                  |
| [**WDI \_ TLV \_ 操作 \_ 框架 \_ 设备 \_ 上下文**](wdi-tlv-action-frame-device-context.md)     |                                | X        | 如果主机决定向此传入消息发送响应，则指定供应商特定的信息，这些信息将向下传递。 为了避免生存期管理问题，IHV 组件不能在此字段中使用指针。 |

 

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

 

 




