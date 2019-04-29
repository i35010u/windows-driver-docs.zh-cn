---
title: WIA\_IPA\_ITEM\_TIME
description: WIA\_IPA\_项\_时间属性包含最初捕获映像的时间。
ms.assetid: 30e29169-7a1a-412e-858a-a467d6f1b44e
keywords:
- WIA_IPA_ITEM_TIME 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51c7ccc26e7194a9ecae08e7cb40172f5a53ac6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388780"
---
# <a name="wiaipaitemtime"></a>WIA\_IPA\_ITEM\_TIME


WIA\_IPA\_项\_时间属性包含最初捕获映像的时间。

## <span id="ddk_wia_ipa_item_time_si"></span><span id="DDK_WIA_IPA_ITEM_TIME_SI"></span>


属性类型：VT\_UI2 | VT\_VECTOR

有效值：WIA\_PROP\_NONE

访问权限：读/写或只读的

<a name="remarks"></a>备注
-------

WIA 微型驱动程序创建和维护 WIA\_IPA\_项\_时间属性。 此属性应报告为 SYSTEMTIME 结构 （它 Microsoft Windows SDK 文档中所述） 的窗体中的八个 WORD 值的向量。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





