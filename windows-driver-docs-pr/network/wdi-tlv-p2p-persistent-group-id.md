---
title: WDI_TLV_P2P_PERSISTENT_GROUP_ID
description: WDI_TLV_P2P_PERSISTENT_GROUP_ID 是一种 TLV，其中包含要用于连接的永久组的组 ID。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PERSISTENT_GROUP_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fc64ef1c617bab70defe3798a6d42c1bbfd710ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818201"
---
# <a name="wdi_tlv_p2p_persistent_group_id"></a>WDI \_ TLV \_ P2P \_ 永久性 \_ 组 \_ ID


WDI \_ tlv \_ P2P \_ 永久性 \_ 组 \_ ID 是一个 tlv，其中包含要用于连接的永久组的组 ID。

## <a name="tlv-type"></a>TLV 类型


0xF1

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                 | 允许多个 TLV 实例 | 可选 | 说明                            |
|----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 设备 \_ 地址**](wdi-tlv-p2p-device-address.md) |                                |          | 组所有者的设备地址。 |
| [**WDI \_ TLV \_ SSID**](wdi-tlv-ssid.md)                               |                                |          | 组 SSID。                        |

 

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

 

 




