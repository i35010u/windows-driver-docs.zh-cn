---
title: WDI_TLV_BAND_INFO
description: WDI_TLV_BAND_INFO 是 TLV 包含带区信息。
ms.assetid: 37F1CE39-5471-489A-8DA2-F058B631B31F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BAND_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9b33eeff65813cddd6bb3df1698fceb938bd3872
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361776"
---
# <a name="wditlvbandinfo"></a>WDI\_TLV\_外\_信息


WDI\_TLV\_外\_信息是包含带区信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x27

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                 | 允许多个 TLV 实例 | 可选 | 描述                                   |
|----------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_外\_功能**](wdi-tlv-band-capabilities.md)    |                                |          | 带区的功能。                 |
| [**WDI\_TLV\_PHY\_TYPE\_LIST**](wdi-tlv-phy-type-list.md)           |                                |          | 在此带区有效 PHY 类型的列表。       |
| [**WDI\_TLV\_CHANNEL\_LIST**](wdi-tlv-channel-list.md)              |                                |          | 在此带区有效频道号的列表。 |
| [**WDI\_TLV\_CHANNEL\_WIDTH\_LIST**](wdi-tlv-channel-width-list.md) |                                |          | 通道宽度，以 mhz 为单位的列表               |

 

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

 

 




