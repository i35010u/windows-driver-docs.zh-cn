---
title: WDI_TLV_AP_BAND_CHANNEL
description: WDI_TLV_AP_BAND_CHANNEL 是一种 TLV，用于指定访问点带和通道信息。
ms.assetid: 5659CFA1-7FA9-490D-83DE-A56A895602A0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_AP_BAND_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 57c8ea3ac6950ff3a4b5a1c425f2daecd73fe50b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206179"
---
# <a name="wdi_tlv_ap_band_channel"></a>WDI \_ TLV \_ AP \_ 频带 \_ 通道


WDI \_ tlv \_ AP \_ 带 \_ 通道是一个 tlv，用于指定访问点带和通道信息。

**注意**   此 TLV 已添加到 Windows 10 版本1511，WDI 版本1.0.10 中。

 

## <a name="tlv-type"></a>TLV 类型


0x127

## <a name="length"></a>Length


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                               | 允许多个 TLV 实例 | 可选 | 说明                                                |
|--------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------|
| [**WDI \_ TLV \_ BANDID**](wdi-tlv-bandid.md)                         |                                |          | 指定带区的标识符。                     |
| [**WDI \_ TLV \_ 通道 \_ 信息 \_ 列表**](wdi-tlv-channel-info-list.md) |                                | X        | 指定要在其上启动访问点的通道的列表。 |

 

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

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 任务 \_ 启动 \_ AP](./oid-wdi-task-start-ap.md)

 

