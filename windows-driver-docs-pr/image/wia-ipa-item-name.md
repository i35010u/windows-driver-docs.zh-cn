---
title: WIA\_IPA\_项\_名称
description: WIA\_IPA\_项\_名称属性包含 WIA 项名称。
ms.assetid: becdd9c6-8202-4c0e-a530-043c1b8421fa
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
ms.openlocfilehash: 3676bed9c12651fecb2fcc29a7036417951814e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840690"
---
# <a name="wia_ipa_item_name"></a>WIA\_IPA\_项\_名称


WIA\_IPA\_项\_名称属性包含 WIA 项名称。

## <span id="ddk_wia_ipa_item_name_si"></span><span id="DDK_WIA_IPA_ITEM_NAME_SI"></span>


属性类型： VT\_BSTR

有效值： WIA\_的\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

*项目名称*与在对[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)服务实用程序的调用中指定的项目名称相同。

应用程序读取 WIA\_IPA\_项\_名称属性，以确定它当前正在使用哪个项。 每个项必须具有唯一的名称。 WIA 服务创建并维护 WIA\_IPA\_项\_名称。

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
<td>Wiadef （包括 Wiadef）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**IWiaMiniDrvTransferCallback：： GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)

[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

 






