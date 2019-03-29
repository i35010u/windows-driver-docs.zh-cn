---
title: WDI_TLV_ACTION_FRAME_DEVICE_CONTEXT
description: WDI_TLV_ACTION_FRAME_DEVICE_CONTEXT 是包含操作帧设备上下文 TLV。
ms.assetid: D8AF374A-0AD0-4856-B05C-B8E3A3F1572B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ACTION_FRAME_DEVICE_CONTEXT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 68fbfd57fee08bdcb3026e95bf2c3ab143d9354b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568952"
---
# <a name="wditlvactionframedevicecontext"></a>WDI\_TLV\_ACTION\_FRAME\_DEVICE\_CONTEXT


WDI\_TLV\_操作\_帧\_设备\_上下文是包含操作帧设备上下文 TLV。

## <a name="tlv-type"></a>TLV 类型


0xAC

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                              |
|-----------|--------------------------------------------------------------------------|
| UINT8\[\] | UINT8 元素数组，其中包含操作帧设备上下文。 |

 

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

 

 




