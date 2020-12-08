---
title: WDI_TLV_HESSID_INFO
description: WDI_TLV_HESSID_INFO 是包含 HESSID 信息的 TLV，其中包括 HESSIDs 列表、访问网络类型和热点指示元素。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_HESSID_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1814937f05bf577f4d360f7e2c864c11e110884d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783789"
---
# <a name="wdi_tlv_hessid_info"></a>WDI \_ TLV \_ HESSID \_ 信息


WDI \_ tlv \_ HESSID \_ INFO 是包含 HESSID 信息的 tlv，其中包括 HESSIDs 的列表、访问网络类型和热点指示元素。

## <a name="tlv-type"></a>TLV 类型


0xFF

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                 | 允许多个 TLV 实例 | 可选 | 说明                                                                              |
|--------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 访问 \_ 网络 \_ 类型**](wdi-tlv-access-network-type.md)               |                                |          | 要用于连接到的网络的探测请求中的访问网络类型。 |
| [**WDI \_ TLV \_ HESSID**](wdi-tlv-hessid.md)                                           |                                |          | 允许端口连接到的 HESSIDs 的列表。                              |
| [**WDI \_ TLV \_ 热点 \_ 指示 \_ 元素**](wdi-tlv-hotspot-indication-element.md) |                                |          | 要在关联请求中使用的热点指示元素。                    |

 

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

 

 




