---
title: WIA\_DIP\_UI\_CLSID
description: WIA\_DIP\_UI\_CLSID 属性包含与 WIA 微型驱动程序一起安装的任何用户界面 (UI) 扩展 COM 对象的供应商提供的类标识符 (CLSID)。 WIA 服务创建并维护此属性。
ms.assetid: 05b2bda0-d53d-44f9-89c0-e0f6f1fc2b48
keywords:
- WIA_DIP_UI_CLSID 成像设备
topic_type:
- apiref
api_name:
- WIA_DIP_UI_CLSID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aeb57f2888f488882a9d2f5f5012b4670d90dff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520396"
---
# <a name="wiadipuiclsid"></a>WIA\_DIP\_UI\_CLSID


WIA\_DIP\_UI\_CLSID 属性包含与 WIA 微型驱动程序一起安装的任何用户界面 (UI) 扩展 COM 对象的供应商提供的类标识符 (CLSID)。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_ui_clsid_si"></span><span id="DDK_WIA_DIP_UI_CLSID_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

包含在 WIA 的 UI CLSID 值\_DIP\_UI\_从驱动程序的 INF 文件获取 CLSID 属性。 如果指定没有 UI CLSID，WIA 服务提供了默认值。 仅在内部使用此属性由 WIA 服务时要显示用户界面。

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

 

 





