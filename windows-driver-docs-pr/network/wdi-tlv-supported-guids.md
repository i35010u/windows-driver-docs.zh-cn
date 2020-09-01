---
title: WDI_TLV_SUPPORTED_GUIDS
description: WDI_TLV_SUPPORTED_GUIDS 是包含受支持的 NDIS GUID 的 TLV。
ms.assetid: 957645EE-A6E3-402E-B18B-B2E7C73D6F6B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SUPPORTED_GUIDS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 51dfc98fb664fafd398d5d95e61f035a0e188358
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216076"
---
# <a name="wdi_tlv_supported_guids"></a>WDI \_ TLV \_ 支持的 \_ GUID


WDI \_ tlv \_ 支持的 \_ guid 是包含受支持的 NDIS GUID 的 tlv。

**注意**   此 TLV 已添加到 Windows 10 版本1607，WDI 版本1.0.21 中。

 

## <a name="tlv-type"></a>TLV 类型


0x130

## <a name="length"></a>Length


[NDIS \_ GUID](./filling-in-an-ndis-guid-structure.md)结构) 大小 (以字节为单位）。

## <a name="values"></a>值


| 类型       | 说明            |
|------------|------------------------|
| NDIS \_ GUID | 支持的 NDIS GUID。 |

 

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

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 获取 \_ 适配器 \_ 功能](./oid-wdi-get-adapter-capabilities.md)

 

