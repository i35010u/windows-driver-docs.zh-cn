---
title: WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE
description: WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE 为 TLV，其中包含请求的关联参数 TLV 类型。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e8b315f6b6eaafb4578035b696b6a70385747986
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840883"
---
# <a name="wdi_tlv_association_parameters_requested_type"></a>WDI \_ TLV \_ 关联 \_ 参数 \_ 请求的 \_ 类型


请求的 WDI \_ tlv \_ 关联 \_ 参数 \_ \_ 类型是包含请求的关联参数 TLV 类型的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xBB

## <a name="length"></a>长度


UINT16 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型       | 描述                                                                                                                                                                                                                                  |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16\[\] | 请求的关联参数 TLV 类型的列表。 有效的 TLV 类型为 [**WDI \_ tlv \_ PMKID**](wdi-tlv-pmkid.md) (0x9F) 和 [**WDI \_ tlv \_ 额外 \_ 关联 \_ 请求 \_**](wdi-tlv-extra-association-request-ies.md) (0x40) 。 |

 

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

 

 




