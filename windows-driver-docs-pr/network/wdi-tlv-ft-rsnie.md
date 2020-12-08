---
title: WDI_TLV_FT_RSNIE
description: WDI_TLV_FT_RSNIE 是包含快速转换 RSN IE 字节 blob 的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_FT_RSNIE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ac1151b6fc53cbc5ff98b767548e9a0d74b90c22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825371"
---
# <a name="wdi_tlv_ft_rsnie"></a>WDI \_ TLV \_ FT \_ RSNIE


WDI \_ tlv \_ FT \_ RSNIE 是一个 tlv，其中包含快速转换 RSN IE 字节 blob。

## <a name="tlv-type"></a>TLV 类型


0x10C

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                    |
|-----------|--------------------------------------------------------------------------------|
| UINT8\[\] | 包含快速转换 RSN IE 字节 blob 的 UINT8 元素数组。 |

 

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

 

 




