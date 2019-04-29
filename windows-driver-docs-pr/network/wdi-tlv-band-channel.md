---
title: WDI_TLV_BAND_CHANNEL
description: WDI_TLV_BAND_CHANNEL 是包含通道扫描指定的带区的 TLV。
ms.assetid: CC3142BE-45CC-4064-A203-ADAF5BE05C01
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BAND_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7b57992389745cb57d3b1b329ba11f37769e58fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361789"
---
# <a name="wditlvbandchannel"></a>WDI\_TLV\_外\_通道


WDI\_TLV\_外\_通道是包含通道扫描指定的带区的 TLV。

## <a name="tlv-type"></a>TLV 类型


0x2C

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                               | 允许多个 TLV 实例 | 可选 | 描述                                                                                     |
|--------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_BANDID**](wdi-tlv-bandid.md)                         |                                |          | 指定的带区的标识符。                                                          |
| [**WDI\_TLV\_CHANNEL\_INFO\_LIST**](wdi-tlv-channel-info-list.md) |                                |          | 指定要扫描的频道的列表。 如果列表为空，该端口必须扫描上的所有通道。 |

 

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

 

 




