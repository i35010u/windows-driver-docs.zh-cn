---
title: '\_启用 WIA IP 的 \_ \_ 条形码 \_ 类型'
description: "\"WIA \\_ ip \\_ 已启用 \\_ 条形码 \\_ 类型\" 属性用于选择条码读取器将在当前会话中搜索的已启用的条码。"
keywords:
- WIA_IPS_ENABLED_BARCODE_TYPES 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ENABLED_BARCODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7b6a878cbac3f1d218e0210b41000b93d7e883f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820219"
---
# <a name="wia_ips_enabled_barcode_types"></a>\_启用 WIA IP 的 \_ \_ 条形码 \_ 类型


" **WIA \_ ip \_ 已启用 \_ 条形码 \_ 类型** " 属性用于选择条码读取器将在当前会话中搜索的已启用的条码。 这些条码可以是 WIA 微型驱动程序为 [**wia \_ IPS \_ \_ \_**](wia-ips-supported-barcode-types.md)报告的一些或所有值。 数组中值的顺序指定了要在其中搜索各个条码的优先级顺序。




属性类型： VT \_ I4 |VT \_ 矢量

有效值： WIA \_ \_ (单个 "array"/vector 值) 

访问权限：读/写

<a name="remarks"></a>备注
-------

" **\_ 启用 wia ip 的 \_ \_ 条形码 \_ 类型** " 属性的有效值与为 \_ \_ " [**wia \_ ips 支持的 \_ \_ 条形码 \_ 类型**](wia-ips-supported-barcode-types.md) " 属性定义的 wia 条形码值相同。

所有条形码读取器项都需要此属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





