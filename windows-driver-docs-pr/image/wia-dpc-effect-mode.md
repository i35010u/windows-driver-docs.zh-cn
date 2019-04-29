---
title: WIA\_DPC\_效果\_模式
description: WIA\_DPC\_效果\_模式属性指定特殊图像采集模式的照相机。
ms.assetid: a874858d-4400-425f-8423-b41bbeb1a925
keywords:
- WIA_DPC_EFFECT_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EFFECT_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f1020b54e82117137b318ce86b9a3787aeaa448
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373108"
---
# <a name="wiadpceffectmode"></a>WIA\_DPC\_效果\_模式


WIA\_DPC\_效果\_模式属性指定特殊图像采集模式的照相机。

## <span id="ddk_wia_dpc_effect_mode_si"></span><span id="DDK_WIA_DPC_EFFECT_MODE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的常量\_DPC\_效果\_模式属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EFECTMODE_BW</p></td>
<td><p>捕获灰度图像</p></td>
</tr>
<tr class="even">
<td><p>EFFECTMODE_SEPIA</p></td>
<td><p>捕获棕褐色映像</p></td>
</tr>
<tr class="odd">
<td><p>EFFECTMODE_STANDARD</p></td>
<td><p>捕获用于相机的标准模式中的图像</p></td>
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
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





