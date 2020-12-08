---
title: WDI_TLV_BAND_ID_LIST
description: WDI_TLV_BAND_ID_LIST 是包含带区 Id 列表的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_BAND_ID_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 44c15d97d10af75705ba5674ade55f0b6bcfd9df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817069"
---
# <a name="wdi_tlv_band_id_list"></a>WDI \_ TLV \_ 波段 \_ ID \_ 列表


WDI \_ tlv \_ 波段 \_ ID \_ 列表是一个 tlv，其中包含带区 id 的列表。

## <a name="tlv-type"></a>TLV 类型


0xB6

## <a name="length"></a>长度


WDI \_ 波段 \_ ID 数组 (UINT32) 元素的数组大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型              | 描述           |
|-------------------|-----------------------|
| WDI \_ 波段 \_ ID\[\] | 带区 Id 的数组。 |

 

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

 

 




