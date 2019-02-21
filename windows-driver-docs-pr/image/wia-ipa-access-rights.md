---
title: WIA\_IPA\_访问\_权限
description: WIA\_IPA\_访问\_权限属性包含 WIA 项的访问权限。
ms.assetid: 5bfa9406-2cb6-4c8b-ab25-6f8f55d941d4
keywords:
- WIA_IPA_ACCESS_RIGHTS 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_ACCESS_RIGHTS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3a44d58a143e5b9fbcdff241959e0bcf744ce61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555140"
---
# <a name="wiaipaaccessrights"></a>WIA\_IPA\_访问\_权限


WIA\_IPA\_访问\_权限属性包含 WIA 项的访问权限。

## <span id="ddk_wia_ipa_access_rights_si"></span><span id="DDK_WIA_IPA_ACCESS_RIGHTS_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_FLAG

访问权限：读/写或只读的 （具体取决于项的功能具有更改其访问权限）

<a name="remarks"></a>备注
-------

*访问权限*控制应用程序，若要删除 WIA 项树中的项的能力。 WIA 微型驱动程序创建和维护 WIA\_IPA\_访问\_权限属性。

下表描述了有效使用 WIA 的常量\_IPA\_访问\_权限。

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
<td><p>WIA_ITEM_CAN_BE_DELETED</p></td>
<td><p>可以删除此 WIA 项。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ITEM_READ</p></td>
<td><p>对项的访问是只读的。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ITEM_WRITE</p></td>
<td><p>对项的访问是读/写。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ITEM_RD</p></td>
<td><p>WIA_ITEM_READ | WIA_ITEM_CAN_BE_DELETED</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ITEM_RWD</p></td>
<td><p>WIA_ITEM_READ | WIA_ITEM_WRITE | WIA_ITEM_CAN_BE_DELETED</p></td>
</tr>
</tbody>
</table>

 

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

 

 





