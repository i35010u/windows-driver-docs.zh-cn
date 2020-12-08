---
title: WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL
description: WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL 是一种 TLV，用于指定探测请求是否应在发现过程中包含侦听通道属性。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f52827ce294239bb797b5f08e59342c32e267e43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818303"
---
# <a name="wdi_tlv_p2p_include_listen_channel"></a>WDI \_ TLV \_ P2P \_ 包含 \_ 侦听 \_ 通道


WDI \_ tlv \_ P2P \_ 包含 \_ 侦听 \_ 通道是一个 tlv，用于指定探测请求是否应在发现过程中包含侦听通道属性。

**注意**  此 TLV 已添加到 Windows 10 版本1607，WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x128

## <a name="length"></a>长度


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型  | 描述                                                                                                                                                           |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 此参数指定探测请求是否应在发现过程中包含侦听通道属性。 有效值为 0 (不包括) 和 1 (包括) 。 |

 

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

 

 




