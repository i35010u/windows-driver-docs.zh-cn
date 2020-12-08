---
title: WIA \_ IPA \_ 访问 \_ 权限
description: WIA \_ IPA \_ access \_ 权限属性包含 wia 项的访问权限。
keywords:
- WIA_IPA_ACCESS_RIGHTS 图像设备
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
ms.openlocfilehash: 7307301b172736699a6e3574760c5b44de1aef64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837733"
---
# <a name="wia_ipa_access_rights"></a>WIA \_ IPA \_ 访问 \_ 权限


WIA \_ IPA \_ access \_ 权限属性包含 wia 项的访问权限。

## <span id="ddk_wia_ipa_access_rights_si"></span><span id="DDK_WIA_IPA_ACCESS_RIGHTS_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 标志

访问权限： "读/写" 或 "只读" (具体取决于项的访问权限更改的能力) 

<a name="remarks"></a>备注
-------

*访问权限* 控制应用程序删除 WIA 项树中的项的能力。 WIA 微型驱动程序创建并维护 WIA \_ IPA \_ 访问 \_ 权限属性。

下表描述了对 WIA \_ IPA 访问权限有效的常量 \_ \_ 。

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
<td><p>此 WIA 项可删除。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ITEM_READ</p></td>
<td><p>对项的访问是只读的。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ITEM_WRITE</p></td>
<td><p>对项的访问是可读/写的。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ITEM_RD</p></td>
<td><p>WIA_ITEM_READ |WIA_ITEM_CAN_BE_DELETED</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ITEM_RWD</p></td>
<td><p>WIA_ITEM_READ |WIA_ITEM_WRITE |WIA_ITEM_CAN_BE_DELETED</p></td>
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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





