---
title: WDI_TLV_IHV_DATA
description: WDI_TLV_IHV_DATA 是一种 TLV，其中包含由 IHV 扩展性模块使用的特定于 IHV 的信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_DATA 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8a1c276065d0d13dc3b0d313c4dc1987a26dcf31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791303"
---
# <a name="wdi_tlv_ihv_data"></a>WDI \_ TLV \_ IHV \_ 数据


WDI \_ tlv \_ IHV \_ 数据是一个 tlv，其中包含由 ihv 扩展性模块使用的特定于 ihv 的信息。

## <a name="tlv-type"></a>TLV 类型


0xBD

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                            |
|-----------|------------------------------------------------------------------------|
| UINT8\[\] | IHV 扩展性模块使用的特定于 IHV 的信息。 |

 

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

 

 




