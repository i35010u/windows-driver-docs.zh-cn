---
title: WIA \_ DIP \_ UI \_ CLSID
description: WIA \_ DIP \_ UI \_ CLSID 属性包含供应商提供的类标识符 (与 WIA 微型驱动程序一起安装的任何用户界面 (UI) 扩展 COM 对象的 CLSID) 。 WIA 服务创建并维护此属性。
keywords:
- WIA_DIP_UI_CLSID 图像设备
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
ms.openlocfilehash: 64164049d3e0ed1aca2d4d75639bcee5c52fedb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824495"
---
# <a name="wia_dip_ui_clsid"></a>WIA \_ DIP \_ UI \_ CLSID


WIA \_ DIP \_ UI \_ CLSID 属性包含供应商提供的类标识符 (与 WIA 微型驱动程序一起安装的任何用户界面 (UI) 扩展 COM 对象的 CLSID) 。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_ui_clsid_si"></span><span id="DDK_WIA_DIP_UI_CLSID_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA DIP UI clsid 属性中包含的 UI CLSID \_ 值 \_ \_ 是从驱动程序的 INF 文件中获取的。 如果未指定 UI CLSID，WIA 服务将提供默认值。 此属性仅在 UI 显示时由 WIA 服务内部使用。

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

 

 





