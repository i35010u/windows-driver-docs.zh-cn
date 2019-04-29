---
title: WDI_TLV_P2P_PERSISTENT_GROUP_ID
description: WDI_TLV_P2P_PERSISTENT_GROUP_ID 是包含要用于连接的永久组的组 ID TLV。
ms.assetid: 0C759D34-3197-4CAB-A691-187BC3457C04
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_PERSISTENT_GROUP_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5b8a7db06565f3ae0122394d86c78be8e453a375
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362817"
---
# <a name="wditlvp2ppersistentgroupid"></a>WDI\_TLV\_P2P\_的永久\_组\_ID


WDI\_TLV\_P2P\_的永久\_组\_ID 是包含要用于连接的永久组的组 ID TLV。

## <a name="tlv-type"></a>TLV 类型


0xF1

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                 | 允许多个 TLV 实例 | 可选 | 描述                            |
|----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------|
| [**WDI\_TLV\_P2P\_DEVICE\_ADDRESS**](wdi-tlv-p2p-device-address.md) |                                |          | 组所有者的设备地址。 |
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid.md)                               |                                |          | 组 SSID。                        |

 

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

 

 




