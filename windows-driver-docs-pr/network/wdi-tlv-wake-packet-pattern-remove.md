---
title: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE
description: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE 是包含的唤醒数据包模式 ID 来删除与 OID_WDI_SET_REMOVE_WOL_PATTERN TLV。
ms.assetid: 69C87D35-AE6B-4F69-B099-A55B65EDAC58
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_PATTERN_REMOVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f6bb3c9578e9396d9ea8b07925bf3eb77dc7fd28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357104"
---
# <a name="wditlvwakepacketpatternremove"></a>WDI\_TLV\_WAKE\_PACKET\_PATTERN\_REMOVE


WDI\_TLV\_唤醒\_数据包\_模式\_删除是包含要删除的唤醒数据包模式 ID TLV [OID\_WDI\_集\_删除\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-remove-wol-pattern)。

## <a name="tlv-type"></a>TLV 类型


0x6B

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                           |
|--------|---------------------------------------|
| UINT32 | 指定唤醒数据包模式 id。 |

 

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

 

 




