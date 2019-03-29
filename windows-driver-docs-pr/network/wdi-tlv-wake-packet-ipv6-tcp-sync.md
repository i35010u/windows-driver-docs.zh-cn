---
title: WDI_TLV_WAKE_PACKET_IPv6_TCP_SYNC
description: WDI_TLV_WAKE_PACKET_IPv6_TCP_SYNC 是包含在 LAN IPv6 TCP 同步数据包信息 TLV。
ms.assetid: CBC0EA08-FDB4-415B-948C-E906F0471AD2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_IPv6_TCP_SYNC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1569cbbf9ec150d963961045a00724ff9b8a6814
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567216"
---
# <a name="wditlvwakepacketipv6tcpsync"></a>WDI\_TLV\_WAKE\_PACKET\_IPv6\_TCP\_SYNC


WDI\_TLV\_唤醒\_数据包\_IPv6\_TCP\_同步是包含在 LAN IPv6 TCP 同步数据包信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x5E

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入        | 描述                                                      |
|-------------|------------------------------------------------------------------|
| UINT32      | 指定 WoL 模式 id。                                    |
| UINT8\[16\] | TCP SYN 数据包中指定的 IPv6 源地址。         |
| UINT8\[16\] | TCP SYN 数据包中指定的 IPv6 目标地址。    |
| UINT16      | TCP SYN 数据包中指定的 TCP 源端口号。      |
| UINT16      | TCP SYN 数据包中指定的 TCP 目标端口号。 |

 

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

 

 




