---
title: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID
description: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID 是包含 LAN 唤醒模式 TLV id。
ms.assetid: 78807D91-189B-4E66-B3DC-500E9A59AEF2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 39a2a8f54951c638b5f121110379580416418d07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376585"
---
# <a name="wditlvwakepacketbitmappatternid"></a>WDI\_TLV\_WAKE\_PACKET\_BITMAP\_PATTERN\_ID


WDI\_TLV\_唤醒\_数据包\_位图\_模式\_ID 是 TLV 包含 LAN 唤醒模式 id。

模式 ID 是一个 OS 提供的值，用于标识的 LAN 唤醒模式并设置为在网络适配器上的 LAN 唤醒模式是唯一的值。 操作系统将 add 发送到基础驱动程序或完成对基础驱动程序的请求之前设置模式 ID。

## <a name="tlv-type"></a>TLV 类型


0xE3

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                 |
|--------|-----------------------------|
| UINT32 | LAN 唤醒模式 id。 |

 

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

## <a name="see-also"></a>请参阅


[OID\_WDI\_SET\_ADD\_WOL\_PATTERN](https://msdn.microsoft.com/library/windows/hardware/dn925858)

 

 




