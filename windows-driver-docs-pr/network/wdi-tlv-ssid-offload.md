---
title: WDI_TLV_SSID_OFFLOAD
description: WDI_TLV_SSID_OFFLOAD 是 TLV 包含 SSID 和有关 SSID 的提示。
ms.assetid: 6CF08BEB-8CEE-4C07-B63B-7FAC7AEAB24F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SSID_OFFLOAD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 88d0076d527ad57cba611b4f2e0e4e98331411a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366643"
---
# <a name="wditlvssidoffload"></a>WDI\_TLV\_SSID\_OFFLOAD


WDI\_TLV\_SSID\_卸载是 TLV 包含 SSID 和有关 SSID 的提示。

## <a name="tlv-type"></a>TLV 类型


0x9E

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                         | 允许多个 TLV 实例 | 可选 | 描述                 |
|------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid.md)                                       |                                |          | SSID。                   |
| [**WDI\_TLV\_UNICAST\_ALGORITHM\_LIST**](wdi-tlv-unicast-algorithm-list.md) |                                |          | 单播算法列表。 |
| [**WDI\_TLV\_CHANNEL\_LIST**](wdi-tlv-channel-list.md)                      |                                |          | 通道列表中。           |

 

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

 

 




