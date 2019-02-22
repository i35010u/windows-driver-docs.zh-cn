---
title: WIA\_IPA\_FULL\_ITEM\_NAME
description: WIA\_IPA\_完整\_项\_NAME 属性包含项目的完整名称 （具有路径信息的项名称）。
ms.assetid: ba034507-264a-4960-80ab-d5cb0daa5c1a
keywords:
- WIA_IPA_FULL_ITEM_NAME 成像设备
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
ms.openlocfilehash: 7a01404a4936b11b24b3cb40e0b4c28de9aea1ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546776"
---
# <a name="wiaipafullitemname"></a>WIA\_IPA\_FULL\_ITEM\_NAME


WIA\_IPA\_完整\_项\_NAME 属性包含项目的完整名称 （具有路径信息的项名称）。

## <span id="ddk_wia_ipa_full_item_name_si"></span><span id="DDK_WIA_IPA_FULL_ITEM_NAME_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

*完整项名称*等同于*bstrFullItemName*参数[ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)服务实用工具函数。 应用程序读取 WIA\_IPA\_完整\_项\_当前正在使用名称属性来确定哪个项以及该项 WIA 项树中的位置。 每个项应具有唯一的名称。 应用程序通常使用完整的项名称来搜索 WIA 项树中的项。 WIA 服务创建和维护 WIA\_IPA\_完整\_项\_名称。

应用程序读取 WIA\_IPA\_完整\_项\_名称来确定它将要接收的图像的格式。 应用程序写入此属性设置的格式。 WIA\_IPA\_完整\_项\_名称取决于[ **WIA\_IPA\_TYMED** ](wia-ipa-tymed.md)属性。 WIA 微型驱动程序创建和维护 WIA\_IPA\_完整\_项\_名称。

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


[**IWiaMiniDrvTransferCallback::GetNextStream**](https://msdn.microsoft.com/library/windows/hardware/jj151551)

[**WIA\_IPA\_TYMED**](wia-ipa-tymed.md)

[**wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)

 

 






