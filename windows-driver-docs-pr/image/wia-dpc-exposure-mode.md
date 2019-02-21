---
title: WIA\_DPC\_暴露\_模式
description: WIA\_DPC\_暴露\_模式属性指示照相机的当前曝光模式。
ms.assetid: 30587d4f-5836-4030-9501-7612aaff58ae
keywords:
- WIA_DPC_EXPOSURE_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69b533ecdd1c4be9efe7a0576e7c0d45dce6a205
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521882"
---
# <a name="wiadpcexposuremode"></a>WIA\_DPC\_暴露\_模式


WIA\_DPC\_暴露\_模式属性指示照相机的当前曝光模式。

## <span id="ddk_wia_dpc_exposure_mode_si"></span><span id="DDK_WIA_DPC_EXPOSURE_MODE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序更改 WIA\_DPC\_暴露\_模式属性来控制照相机设备的曝光模式。

下表描述了有效使用 WIA 的常量\_DPC\_暴露\_模式。

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
<td><p>EXPOSUREMODE_APERTURE_PRIORITY</p></td>
<td><p>用户手动设置 aperture，并将相机的设备自动设置快门速度。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_AUTO</p></td>
<td><p>照相机设备会自动设置 aperture 和快门速度。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_MANUAL</p></td>
<td><p>用户手动设置 aperture 和快门速度。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_PROGRAM_ACTION</p></td>
<td><p>照相机设备将自动设置 aperture 和快门速度和优化移动行业 （即，包含快速动作的场景）。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_PROGRAM_CREATIVE</p></td>
<td><p>照相机设备将自动设置 aperture 和快门速度和优化仍使用者而言。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_PORTRAIT</p></td>
<td><p>照相机设备将自动设置 aperture 和快门速度和优化的纵向摄影。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_SHUTTER_PRIORITY</p></td>
<td><p>用户手动设置的快门速度，并将相机的设备自动设置 aperture。</p></td>
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

 

 





