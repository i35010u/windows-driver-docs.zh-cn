---
title: WDI_TLV_COUNTRY_REGION_LIST
description: WDI_TLV_COUNTRY_REGION_LIST 为 TLV，其中包含国家或地区代码的列表。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_COUNTRY_REGION_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1305760868de79a5c4a7a1615d12e8fb9734aef8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837893"
---
# <a name="wdi_tlv_country_region_list"></a>WDI \_ TLV \_ 国家/地区 \_ \_ 列表


WDI \_ tlv \_ 国家 \_ 地区 \_ 列表是包含国家或地区代码列表的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x12

## <a name="length"></a>长度


WDI \_ COUNTRY \_ REGION LIST 元素数组的大小 (以字节为单位) \_ 。 数组必须包含1个或多个元素。

**注意**  WDI \_ 国家/地区 \_ \_ 列表不是 WDI 结构。 它在 WDI TLV 分析程序生成器中定义，仅用于文档目的。

 

## <a name="values"></a>值


| 类型                           | 描述                          |
|--------------------------------|--------------------------------------|
| WDI \_ 国家/地区 \_ \_ 列表\[\] | 国家/地区代码的数组。 |

 

WDI \_ COUNTRY \_ REGION \_ LIST 包含以下元素。

| 类型       | 描述               |
|------------|---------------------------|
| UINT8 \[ 3\] | 国家或地区代码。 |

 

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

 

 




