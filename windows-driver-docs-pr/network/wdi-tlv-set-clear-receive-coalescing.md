---
title: WDI_TLV_SET_CLEAR_RECEIVE_COALESCING
description: WDI_TLV_SET_CLEAR_RECEIVE_COALESCING 为 TLV，其中包含 OID_WDI_SET_CLEAR_RECEIVE_COALESCING 的筛选器 ID。
ms.assetid: 4AF7A1A4-A1B4-48AD-9989-B9E317F93459
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_CLEAR_RECEIVE_COALESCING 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4f9eeadf33f002df1aafea19b6efd241e710f16d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212673"
---
# <a name="wdi_tlv_set_clear_receive_coalescing"></a>WDI \_ TLV \_ 设置 \_ 清除 \_ 接收 \_ 合并


WDI \_ tlv \_ 设置 \_ 清除 \_ 接收 \_ 合并是一个 TLV，其中包含 [OID \_ WDI \_ SET \_ CLEAR \_ RECEIVE \_ 合并](./oid-wdi-set-clear-receive-coalescing.md)的筛选器 ID。

## <a name="tlv-type"></a>TLV 类型


0x9B

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明           |
|--------|-----------------------|
| UINT32 | 筛选器的 ID。 |

 

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

 

