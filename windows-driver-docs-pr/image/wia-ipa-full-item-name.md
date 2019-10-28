---
title: WIA\_IPA\_完整\_项\_名称
description: WIA\_IPA\_FULL\_项\_NAME 属性包含完整的项名称（包含路径信息的项名称）。
ms.assetid: ba034507-264a-4960-80ab-d5cb0daa5c1a
keywords:
- WIA_IPA_FULL_ITEM_NAME 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_FULL_ITEM_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce543f670529d6e89f384eea3411826ad7504d61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840696"
---
# <a name="wia_ipa_full_item_name"></a>WIA\_IPA\_完整\_项\_名称


WIA\_IPA\_FULL\_项\_NAME 属性包含完整的项名称（包含路径信息的项名称）。

## <span id="ddk_wia_ipa_full_item_name_si"></span><span id="DDK_WIA_IPA_FULL_ITEM_NAME_SI"></span>


属性类型： VT\_BSTR

有效值： WIA\_的\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

*完整的项名称*与[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)服务实用工具函数的*bstrFullItemName*参数相同。 应用程序读取 WIA\_IPA\_FULL\_项\_NAME 属性，以确定它当前使用的项以及该项在 WIA 项树中的位置。 每个项都应具有唯一的名称。 应用程序通常使用完整项名称在 WIA 项树中搜索项。 WIA 服务创建并维护 WIA\_IPA\_完整\_项\_名称。

应用程序读取 WIA\_IPA\_FULL\_项\_名称，以确定要接收的图像的格式。 应用程序写入此属性以设置格式。 WIA\_IPA\_完整\_项\_名称取决于[**WIA\_IPA\_TYMED**](wia-ipa-tymed.md)属性。 WIA 微型驱动程序创建并维护 WIA\_IPA\_完整\_项\_名称。

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

[**WIA\_IPA\_TYMED**](wia-ipa-tymed.md)

[**wiasCreateDrvItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

 






