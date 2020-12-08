---
title: WDI_TLV_IHV_NON_WDI_OIDS_LIST
description: WDI_TLV_IHV_NON_WDI_OIDS_LIST 是一种 TLV，其中包含适配器要播发到操作系统的非 WDI Oid 的列表。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_NON_WDI_OIDS_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aa859f3135041dac0e9bbe2e78ce10357757bad1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791301"
---
# <a name="wdi_tlv_ihv_non_wdi_oids_list"></a>WDI \_ TLV \_ IHV \_ 非 \_ WDI \_ OID \_ LIST


WDI \_ tlv \_ IHV \_ 非 \_ WDI \_ oid \_ list 是一个 TLV，其中包含适配器要播发到操作系统的非 WDI oid 的列表。

## <a name="tlv-type"></a>TLV 类型


0x104

## <a name="length"></a>长度


UINT32 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型       | 描述                                                                                                                                                                                       |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32\[\] | 适配器要播发到操作系统的非 WDI Oid 的列表。 适配器不应假定操作系统已将非 WDI Oid 筛选为与此列表匹配。 |

 

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

 

 




