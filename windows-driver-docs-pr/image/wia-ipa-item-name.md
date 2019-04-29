---
title: WIA\_IPA\_ITEM\_NAME
description: WIA\_IPA\_项\_NAME 属性包含 WIA 项名称。
ms.assetid: becdd9c6-8202-4c0e-a530-043c1b8421fa
keywords:
- WIA_IPA_ITEM_NAME 成像设备
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
ms.openlocfilehash: a726e74ca35d381bceeac0fa9eb74a6748cdedda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388784"
---
# <a name="wiaipaitemname"></a>WIA\_IPA\_ITEM\_NAME


WIA\_IPA\_项\_NAME 属性包含 WIA 项名称。

## <span id="ddk_wia_ipa_item_name_si"></span><span id="DDK_WIA_IPA_ITEM_NAME_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

*项目名称*调用中指定的项名称相同[ **wiasCreateDrvItem** ](https://msdn.microsoft.com/library/windows/hardware/ff549160)服务实用工具函数。

应用程序读取 WIA\_IPA\_项\_当前正在使用名称属性来确定哪个项。 每个项必须具有唯一的名称。 WIA 服务创建和维护 WIA\_IPA\_项\_名称。

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

## <a name="see-also"></a>请参阅


[**IWiaMiniDrvTransferCallback::GetNextStream**](https://msdn.microsoft.com/library/windows/hardware/jj151551)

[**wiasCreateDrvItem**](https://msdn.microsoft.com/library/windows/hardware/ff549160)

 

 






