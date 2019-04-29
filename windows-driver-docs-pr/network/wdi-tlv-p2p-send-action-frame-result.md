---
title: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT
description: WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT 是 TLV，其中包含有关对等方发送操作帧的信息。
ms.assetid: DA469DF2-4C59-495C-A4B5-DC7B3B157566
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SEND_ACTION_FRAME_RESULT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d73c9f22df88fee3ea81ac7d4c4b6abd0eaf68b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370947"
---
# <a name="wditlvp2psendactionframeresult"></a>WDI\_TLV\_P2P\_发送\_操作\_帧\_结果


WDI\_TLV\_P2P\_发送\_操作\_帧\_结果是 TLV，其中包含有关对等方发送操作帧的信息。

## <a name="tlv-type"></a>TLV 类型


0xAF

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                              | 允许多个 TLV 实例 | 可选 | 描述                                           |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------|
| [**WDI\_TLV\_P2P\_发送\_操作\_帧\_结果\_参数**](wdi-tlv-p2p-send-action-frame-result-parameters.md) |                                |          | Wi-Fi Direct 发送操作帧结果参数。 |
| [**WDI\_TLV\_P2P\_ACTION\_FRAME\_IES**](wdi-tlv-p2p-action-frame-ies.md)                                         |                                |          | 导致浏览器发送到远程设备的组。             |

 

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

 

 




