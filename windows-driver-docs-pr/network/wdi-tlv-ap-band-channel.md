---
title: WDI_TLV_AP_BAND_CHANNEL
description: WDI_TLV_AP_BAND_CHANNEL 是 TLV，指定访问点外和通道信息。
ms.assetid: 5659CFA1-7FA9-490D-83DE-A56A895602A0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AP_BAND_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8da2db372b59d25c5560309e8ceb30f4143308b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374552"
---
# <a name="wditlvapbandchannel"></a>WDI\_TLV\_AP\_BAND\_CHANNEL


WDI\_TLV\_AP\_外\_通道是 TLV，指定访问点外和通道信息。

**请注意**  此 TLV 添加 Windows 10，版本 1511，WDI 版本 1.0.10 中。

 

## <a name="tlv-type"></a>TLV 类型


0x127

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                               | 允许多个 TLV 实例 | 可选 | 描述                                                |
|--------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------|
| [**WDI\_TLV\_BANDID**](wdi-tlv-bandid.md)                         |                                |          | 指定的带区的标识符。                     |
| [**WDI\_TLV\_CHANNEL\_INFO\_LIST**](wdi-tlv-channel-info-list.md) |                                | X        | 指定通道上启动的访问点的列表。 |

 

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


[OID\_WDI\_TASK\_START\_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)

 

 




