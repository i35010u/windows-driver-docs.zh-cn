---
title: WDI_TLV_FT_MDE
description: WDI_TLV_FT_MDE 是包含 BSS 条目 MDIE 的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_MDE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f6f79353716f88b15177e7eaa5e8042d9543a7d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812799"
---
# <a name="wdi_tlv_ft_mde"></a>WDI \_ TLV \_ FT \_ MDE


WDI \_ tlv \_ FT \_ MDE 是一个 tlv，其中包含 BSS 项的 MDIE。

## <a name="tlv-type"></a>TLV 类型


0x10D

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述              |
|-----------|--------------------------|
| UINT8\[\] | BSS 项的 MDIE。 |

 

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

 

 




