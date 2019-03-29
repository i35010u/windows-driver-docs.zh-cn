---
title: WDI_TLV_P2P_ACTION_FRAME_IES
description: WDI_TLV_P2P_ACTION_FRAME_IES 是包含操作帧 IEs TLV。
ms.assetid: 7F5DD866-AD7D-4E3E-B352-78FAE4AFD995
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ACTION_FRAME_IES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bd10a7237c03759fc6df127de245fd0a406b5cb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575750"
---
# <a name="wditlvp2pactionframeies"></a>WDI\_TLV\_P2P\_操作\_帧\_导致浏览器


WDI\_TLV\_P2P\_操作\_帧\_导致浏览器是包含操作帧 IEs TLV。

## <a name="tlv-type"></a>TLV 类型


0x90

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| UINT8\[\] | 指定一组发送到远程设备的 Ie 的 UINT8 元素的数组。 |

 

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

 

 




