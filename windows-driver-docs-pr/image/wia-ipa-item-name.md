---
title: WIA \_ IPA \_ 项 \_ 名称
description: WIA \_ IPA \_ item \_ NAME 属性包含 wia 项名称。
keywords:
- WIA_IPA_ITEM_NAME 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6df5381ecd351faa569183a9e849118eebf0a8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817287"
---
# <a name="wia_ipa_item_name"></a>WIA \_ IPA \_ 项 \_ 名称


WIA \_ IPA \_ item \_ NAME 属性包含 wia 项名称。

## <span id="ddk_wia_ipa_item_name_si"></span><span id="DDK_WIA_IPA_ITEM_NAME_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

*项目名称* 与在对 [**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)服务实用程序的调用中指定的项目名称相同。

应用程序读取 WIA \_ IPA \_ 项 \_ 名称属性，以确定它当前正在使用哪个项。 每个项必须具有唯一的名称。 WIA 服务创建并维护 WIA \_ IPA \_ ITEM \_ NAME。

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


[**IWiaMiniDrvTransferCallback：： GetNextStream**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)

[**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

