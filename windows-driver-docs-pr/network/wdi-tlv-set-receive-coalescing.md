---
title: WDI_TLV_SET_RECEIVE_COALESCING
description: WDI_TLV_SET_RECEIVE_COALESCING 是包含收到的 OID_WDI_SET_RECEIVE_COALESCING 的数据包合并参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SET_RECEIVE_COALESCING 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c4f75973b4f8c712cff5165671ca1f34e0c5de5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821973"
---
# <a name="wdi_tlv_set_receive_coalescing"></a>WDI \_ TLV \_ 设置 \_ 接收 \_ 合并


WDI \_ tlv \_ 设置 \_ 接收 \_ 合并是一个 TLV，其中包含已接收的用于 [OID \_ WDI \_ 集 \_ 接收 \_ 合并](./oid-wdi-set-receive-coalescing.md)的数据包合并参数。

## <a name="tlv-type"></a>TLV 类型


0x64

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                               | 允许多个 TLV 实例 | 可选 | 说明                                |
|------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------|
| [**WDI \_ TLV \_ 接收 \_ 合并 \_ 配置**](wdi-tlv-receive-coalescing-config.md) |                                |          | 指定合并筛选器配置。 |
| [**WDI \_ TLV \_ 接收 \_ 筛选器 \_ 字段**](wdi-tlv-receive-filter-field.md)           | X                              | X        | 指定接收筛选器字段。          |

 

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

 

