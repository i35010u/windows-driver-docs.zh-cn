---
title: WIA\_DPC\_焦点\_模式
description: WIA\_DPC\_焦点\_模式属性定义摄像机设备的当前焦点模式下设置。
ms.assetid: d651c9f7-97ca-4fa5-bc52-2af1f7c2e241
keywords:
- WIA_DPC_FOCUS_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_FOCUS_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdbc16569ea16224d43678f9b3418421099343eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524857"
---
# <a name="wiadpcfocusmode"></a>WIA\_DPC\_焦点\_模式


WIA\_DPC\_焦点\_模式属性定义摄像机设备的当前焦点模式下设置。

## <span id="ddk_wia_dpc_focus_mode_si"></span><span id="DDK_WIA_DPC_FOCUS_MODE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

设备驱动程序枚举支持的值的 WIA\_DPC\_焦点\_模式属性和应用程序将此属性设置为照相机设备焦点模式下的写入。

下表描述了有效使用 WIA 的常量\_DPC\_焦点\_模式属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FOCUSMODE_AUTO</p></td>
<td><p>照相机设备自动配置为焦点。</p></td>
</tr>
<tr class="even">
<td><p>FOCUSMODE_MACROAUTO</p></td>
<td><p>照相机设备配置为通过使用短程宏设置自动集中。</p></td>
</tr>
<tr class="odd">
<td><p>FOCUSMODE_MANUAL</p></td>
<td><p>照相机设备配置为手动允许专注于用户。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





