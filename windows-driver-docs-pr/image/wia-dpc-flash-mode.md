---
title: WIA\_DPC\_闪存\_模式
description: WIA\_DPC\_闪存\_模式属性定义摄像机设备的当前闪存模式设置。 设备驱动程序枚举支持此属性的值，并应用程序写入此属性设置为照相机设备的闪存模式。
ms.assetid: 04c58111-09a7-4cd0-b60b-a65197c0931d
keywords:
- WIA_DPC_FLASH_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_FLASH_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 540a507e05defd8be5fc72e385815bbf6824a7a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521346"
---
# <a name="wiadpcflashmode"></a>WIA\_DPC\_闪存\_模式


WIA\_DPC\_闪存\_模式属性定义摄像机设备的当前闪存模式设置。 设备驱动程序枚举支持此属性的值，并应用程序写入此属性设置为照相机设备的闪存模式。

## <span id="ddk_wia_dpc_flash_mode_si"></span><span id="DDK_WIA_DPC_FLASH_MODE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

下表描述了与此属性有效值的六个。

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
<td><p>FLASHMODE_AUTO</p></td>
<td><p>照相机设备确定正确的闪存设置。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_EXTERNALSYNC</p></td>
<td><p>照相机设备配置为与外部 flash 单位同步。</p></td>
</tr>
<tr class="odd">
<td><p>FLASHMODE_FILL</p></td>
<td><p>照相机设备配置闪烁，而不考虑当前的光照条件。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_OFF</p></td>
<td><p>照相机设备配置<em>不</em>闪烁，以执行任何图片。</p></td>
</tr>
<tr class="odd">
<td><p>FLASHMODE_REDEYE_AUTO</p></td>
<td><p>照相机设备使用红眼，而不考虑当前的光照条件来确定正确的闪存设置。</p></td>
</tr>
<tr class="even">
<td><p>FLASHMODE_REDEYE_FILL</p></td>
<td><p>照相机设备配置为使用红眼和 flash 而不考虑当前的光照条件。</p></td>
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

 

 





