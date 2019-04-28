---
title: WDI_TLV_P2P_INCOMING_FRAME_INFORMATION
description: WDI_TLV_P2P_INCOMING_FRAME_INFORMATION 是包含传入 Wi-Fi Direct 操作帧信息 TLV。
ms.assetid: 7E7EF56D-625B-4B79-9AE4-A9C9B7C8547A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INCOMING_FRAME_INFORMATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9fc6067b325e4778a6cfe4e0c2fd09b9be2ca9cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342577"
---
# <a name="wditlvp2pincomingframeinformation"></a>WDI\_TLV\_P2P\_传入\_帧\_信息


WDI\_TLV\_P2P\_传入\_帧\_信息是包含传入 Wi-Fi Direct 操作帧信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x79

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_INCOMING\_FRAME\_PARAMETERS**](wdi-tlv-p2p-incoming-frame-parameters.md) |                                |          | 指定传入的帧参数。                                                                                                                                                                                        |
| [**WDI\_TLV\_P2P\_ACTION\_FRAME\_IES**](wdi-tlv-p2p-action-frame-ies.md)                   |                                |          | 指定接收到的公共操作帧的导致浏览器部分。                                                                                                                                                                  |
| [**WDI\_TLV\_ACTION\_FRAME\_DEVICE\_CONTEXT**](wdi-tlv-action-frame-device-context.md)     |                                | X        | 指定如果主机决定将响应发送到此传入消息传递回下的特定于供应商的信息。 若要避免生存期管理问题，IHV 组件必须在此字段中不使用指针。 |

 

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

 

 




