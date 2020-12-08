---
title: '\_启用 WIA IP 的 \_ \_ 修补程序 \_ 代码 \_ 类型'
description: 启用 WIA \_ IPS \_ " \_ 修补程序 \_ 代码 \_ 类型" 属性用于选择修补程序代码读取器将在当前会话中搜索的已启用的修补程序代码。
keywords:
- WIA_IPS_ENABLED_PATCH_CODE_TYPES 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ENABLED_PATCH_CODE_TYPES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c60190077b17186b01f3477f45e386657346af8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837243"
---
# <a name="wia_ips_enabled_patch_code_types"></a>\_启用 WIA IP 的 \_ \_ 修补程序 \_ 代码 \_ 类型


**启用 WIA \_ IPS \_ " \_ 修补程序 \_ 代码 \_ 类型**" 属性用于选择修补程序代码读取器将在当前会话中搜索的已启用的修补程序代码。 这些修补程序代码可以是 WIA 微型驱动程序为 [**wia \_ ip \_ 支持的 \_ 修补程序 \_ 代码 \_ 类型**](wia-ips-supported-patch-code-types.md)报告的部分或全部值。 数组中值的顺序指定了要在其中搜索各个修补程序代码的优先级顺序。




属性类型： VT \_ I4 |VT \_ 矢量

有效值： WIA \_ \_ (单个 "array"/vector 值) 

访问权限：读/写

<a name="remarks"></a>备注
-------

" **启用了 wia ips 的 \_ \_ \_ 修补程序 \_ 代码 \_ 类型** " 属性的有效值与为 \_ \_ \_ " [**wia \_ ips 支持的 \_ \_ 修补程序 \_ 代码 \_ 类型**](wia-ips-supported-patch-code-types.md) " 属性定义的 wia 修补程序代码值相同。

所有修补程序代码读取器项都需要此属性。

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

 

 





