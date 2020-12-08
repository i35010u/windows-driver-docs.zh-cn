---
title: WIA \_ DPC \_ 曝光 \_ 模式
description: WIA \_ DPC \_ 曝露 \_ 模式属性指示相机的当前曝光模式。
keywords:
- WIA_DPC_EXPOSURE_MODE 图像设备
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
ms.openlocfilehash: be820df0a217689744381dc60a12e275e8b715a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830461"
---
# <a name="wia_dpc_exposure_mode"></a>WIA \_ DPC \_ 曝光 \_ 模式


WIA \_ DPC \_ 曝露 \_ 模式属性指示相机的当前曝光模式。

## <span id="ddk_wia_dpc_exposure_mode_si"></span><span id="DDK_WIA_DPC_EXPOSURE_MODE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序更改 "WIA \_ DPC \_ 曝光 \_ 模式" 属性以控制照相机设备的曝光模式。

下表介绍了在 WIA \_ DPC \_ 曝光模式下有效的常量 \_ 。

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
<td><p>用户手动设置口径，照相机设备会自动设置快门速度。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_AUTO</p></td>
<td><p>照相机设备自动设置口径和快门速度。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_MANUAL</p></td>
<td><p>用户手动设置口径和快门速度。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_PROGRAM_ACTION</p></td>
<td><p>照相机设备会自动设置口径和快门速度，并对其进行优化，以移动 (，即包含快速运动) 的场景。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_PROGRAM_CREATIVE</p></td>
<td><p>照相机设备会自动设置口径和快门速度，并对其进行优化，使其保持不受影响。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMODE_PORTRAIT</p></td>
<td><p>照相机设备自动设置口径和快门速度，并为纵向照片优化它们。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMODE_SHUTTER_PRIORITY</p></td>
<td><p>用户手动设置快门速度，照相机设备自动设置口径。</p></td>
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
<td><p>在 Windows Vista 和更高版本的操作系统中已过时，不应再使用。 但是，在 Windows Vista 中仍定义此属性，以与为 Windows Server 2003、Windows XP 和 windows 的早期版本设计的应用程序和设备兼容。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





