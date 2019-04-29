---
title: WDI_TLV_WAKE_PACKET_MAGIC_PACKET
description: WDI_TLV_WAKE_PACKET_MAGIC_PACKET 是包含 OID_WDI_SET_ADD_WOL_PATTERN 幻数据包的模式 ID TLV。
ms.assetid: F1DEB65B-8DD4-4D4A-9DCB-950C3B562F0A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_MAGIC_PACKET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2f62b79a89d92e1158ffa8d21b71e96adafbed13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382135"
---
# <a name="wditlvwakepacketmagicpacket"></a>WDI\_TLV\_唤醒\_数据包\_MAGIC\_数据包


WDI\_TLV\_唤醒\_数据包\_MAGIC\_数据包是包含的幻数据包的模式 ID TLV [OID\_WDI\_设置\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/dn925858)。

## <a name="tlv-type"></a>TLV 类型


0x5C

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                        |
|--------|----------------------------------------------------|
| UINT32 | 指定 LAN 唤醒的幻数据包模式 id。 |

 

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

 

 




