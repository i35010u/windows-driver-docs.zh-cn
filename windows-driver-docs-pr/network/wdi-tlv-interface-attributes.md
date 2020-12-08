---
title: WDI_TLV_INTERFACE_ATTRIBUTES
description: WDI_TLV_INTERFACE_ATTRIBUTES 是包含接口特性的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INTERFACE_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b112780c93b008cb4d652972dcc5631105053c79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828429"
---
# <a name="wdi_tlv_interface_attributes"></a>WDI \_ TLV \_ 接口 \_ 属性


WDI \_ tlv \_ 接口 \_ 特性是包含接口特性的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x21

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                         | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                     |
|------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 接口 \_ 功能**](wdi-tlv-interface-capabilities.md)  |                                |          | 接口的功能。                                                                                                                                                              |
| [**WDI \_ TLV \_ 固件 \_ 版本**](wdi-tlv-firmware-version.md)              |                                |          | 指定固件版本的 ASCII 字符串。                                                                                                                                            |
| [**WDI \_ TLV \_ IHV \_ 非 \_ WDI \_ OID \_ LIST**](wdi-tlv-ihv-non-wdi-oids-list.md) |                                | X        | 适配器要播发到操作系统的非 WDI Oid 列表。 适配器不应假定操作系统已将非 WDI Oid 筛选为与此列表匹配。 |

 

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

 

 




