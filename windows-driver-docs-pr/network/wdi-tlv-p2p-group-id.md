---
title: WDI_TLV_P2P_GROUP_ID
description: WDI_TLV_P2P_GROUP_ID 是包含 Wi-Fi Direct 中转的组 ID 的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GROUP_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c96c95b97ba3d52655cd3fb4717ca1c3f55341fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818273"
---
# <a name="wdi_tlv_p2p_group_id"></a>WDI \_ TLV \_ P2P \_ 组 \_ ID


WDI \_ tlv \_ P2P \_ 组 \_ id 是一个 tlv，其中包含 Wi-Fi DIRECT 中转的组 ID。

## <a name="tlv-type"></a>TLV 类型


0x75

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                          |
|----------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 设备 \_ 地址**](wdi-tlv-p2p-device-address.md) |                                |          | 指定 Wi-Fi Direct 中转的设备地址。 |
| [**WDI \_ TLV \_ SSID**](wdi-tlv-ssid-list.md)                          |                                |          | 指定组 SSID。                            |

 

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

 

 




