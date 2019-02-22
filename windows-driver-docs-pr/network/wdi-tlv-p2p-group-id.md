---
title: WDI_TLV_P2P_GROUP_ID
description: WDI_TLV_P2P_GROUP_ID 是 TLV Wi-Fi Direct go 包含组的 ID。
ms.assetid: 5DF5E7AA-4A5A-4AF5-90E6-40791C8DBB56
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GROUP_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bdc87b13b3bdd8fe62cba53f8c92317f7316c79c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524799"
---
# <a name="wditlvp2pgroupid"></a>WDI\_TLV\_P2P\_GROUP\_ID


WDI\_TLV\_P2P\_组\_ID 是 TLV Wi-Fi Direct go 包含组的 ID。

## <a name="tlv-type"></a>TLV 类型


0x75

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                          |
|----------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------|
| [**WDI\_TLV\_P2P\_DEVICE\_ADDRESS**](wdi-tlv-p2p-device-address.md) |                                |          | 指定 Wi-Fi Direct 转的设备地址。 |
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid-list.md)                          |                                |          | 指定 SSID 的组。                            |

 

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
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




