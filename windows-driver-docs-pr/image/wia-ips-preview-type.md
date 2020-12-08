---
title: WIA \_ IP \_ 预览 \_ 类型
description: WIA \_ ip \_ 预览 \_ 类型属性指示是否更改 wia \_ IPA \_ 数据类型和 wia \_ IPA \_ 深度，而无需请求新的预览扫描。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PREVIEW_TYPE 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PREVIEW_TYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d5772c33d7cdf4a9f66c8c8e89113f486dca81
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839091"
---
# <a name="wia_ips_preview_type"></a>WIA \_ IP \_ 预览 \_ 类型


WIA \_ ip \_ 预览 \_ 类型属性指示是否更改 [**wia \_ IPA \_ 数据类型**](wia-ipa-datatype.md) 和 [**wia \_ IPA \_ 深度**](wia-ipa-depth.md) ，而无需请求新的预览扫描。 WIA 微型驱动程序创建并维护此属性。

属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

下表介绍了在 "WIA \_ ip \_ 预览类型" 属性中有效的常量 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_ADVANCED_PREVIEW</p></td>
<td><p>支持实时预览更新。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BASIC_PREVIEW</p></td>
<td><p>预览图像只能使用新的预览扫描进行更新。</p></td>
</tr>
</tbody>
</table>

 

**注意**   WIA \_ ip \_ 预览 \_ 类型仅应描述 [**Wia \_ IPA \_ DATATYPE**](wia-ipa-datatype.md) 和 [**wia \_ IPA \_ DEPTH**](wia-ipa-depth.md) 属性。

 

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

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ 数据类型**](wia-ipa-datatype.md)

[**WIA \_ IPA \_ 深度**](wia-ipa-depth.md)

 

 






