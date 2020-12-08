---
title: WDI_TLV_VIRTUALIZATION_ATTRIBUTES
description: WDI_TLV_VIRTUALIZATION_ATTRIBUTES 是包含虚拟化特性的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_VIRTUALIZATION_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8fa76a06342217304427aace2c8d3b4022b89a14
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821947"
---
# <a name="wdi_tlv_virtualization_attributes"></a>WDI \_ TLV \_ 虚拟化 \_ 属性


WDI \_ tlv \_ 虚拟化 \_ 属性是包含虚拟化属性的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x24

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                  | 允许多个 TLV 实例 | 可选 | 说明                      |
|---------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------|
| [**WDI \_ TLV \_ 虚拟化 \_ 功能**](wdi-tlv-virtualization-capabilities.md) |                                |          | 虚拟化功能。 |

 

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

 

 




