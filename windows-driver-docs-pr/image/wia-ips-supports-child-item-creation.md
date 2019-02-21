---
title: WIA\_IPS\_支持\_子\_项\_创建
description: WIA\_IPS\_支持\_子\_项\_创建属性指示设备是否支持子项目的创建。
ms.assetid: 77358889-d2c4-410f-b553-2dae2f7b27e3
keywords:
- WIA_IPS_SUPPORTS_CHILD_ITEM_CREATION 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SUPPORTS_CHILD_ITEM_CREATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1940ad102a88f5195051faeb81026569544740d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548317"
---
# <a name="wiaipssupportschilditemcreation"></a>WIA\_IPS\_支持\_子\_项\_创建


WIA\_IPS\_支持\_子\_项\_创建属性指示设备是否支持子项目的创建。 WIA 微型驱动程序创建并维护此属性

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

支持的项[ **WIA\_IPS\_分段**](wia-ips-segmentation.md)属性和 WIA\_使用\_分段\_筛选器值必须此外支持 WIA\_IPS\_支持\_子\_项\_创建属性，并将其设置为**TRUE**。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WIA\_IP\_分段**](wia-ips-segmentation.md)

 

 






