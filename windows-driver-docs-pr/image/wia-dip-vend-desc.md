---
title: WIA\_DIP\_VEND\_DESC
description: WIA\_DIP\_VEND\_DESC 属性包含 WIA 微型驱动程序供应商说明字符串。 WIA 服务创建并维护此属性。
ms.assetid: 80bb6a4e-3391-4681-93d0-8b60774dfc3d
keywords:
- WIA_DIP_VEND_DESC 成像设备
topic_type:
- apiref
api_name:
- WIA_DIP_VEND_DESC
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4690b204e2810d2cd9097169f083f7bc921a95da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325281"
---
# <a name="wiadipvenddesc"></a>WIA\_DIP\_VEND\_DESC


WIA\_DIP\_VEND\_DESC 属性包含 WIA 微型驱动程序供应商说明字符串。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_vend_desc_si"></span><span id="DDK_WIA_DIP_VEND_DESC_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

供应商说明是从 INF 文件中获取。 应用程序读取 WIA\_DIP\_VEND\_DESC 属性来获取设备供应商的说明。

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

 

 





