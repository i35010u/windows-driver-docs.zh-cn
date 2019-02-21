---
title: WIA\_IPS\_预览\_类型
description: WIA\_IPS\_预览版\_类型属性指示如果 WIA\_IPA\_数据类型和 WIA\_IPA\_深度被更改，而无需请求新的预览扫描。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 2d4f1052-da7a-404e-b462-9a7c2e2caf80
keywords:
- WIA_IPS_PREVIEW_TYPE 成像设备
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
ms.openlocfilehash: 437810cba29f462a053a8e648ae5dbedb3afa999
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543367"
---
# <a name="wiaipspreviewtype"></a>WIA\_IPS\_预览\_类型


WIA\_IPS\_预览版\_类型属性指示如果[ **WIA\_IPA\_数据类型**](wia-ipa-datatype.md)和[ **WIA\_IPA\_深度**](wia-ipa-depth.md)被更改，而无需请求新的预览扫描。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的常量\_IPS\_预览\_类型属性。

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
<td><p>实时的预览支持更新。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BASIC_PREVIEW</p></td>
<td><p>可以仅使用新的预览扫描更新预览图像。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   WIA\_IPS\_预览\_类型应只描述[ **WIA\_IPA\_数据类型**](wia-ipa-datatype.md)并[ **WIA\_IPA\_深度**](wia-ipa-depth.md)属性。

 

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_IPA\_DATATYPE**](wia-ipa-datatype.md)

[**WIA\_IPA\_DEPTH**](wia-ipa-depth.md)

 

 






