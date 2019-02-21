---
title: WIA\_DPC\_暴露\_计量\_模式
description: WIA\_DPC\_暴露\_计量\_模式属性指定用于自动调整曝光度设置照相机的模式。
ms.assetid: f1340ba2-984e-41a1-a6f2-56639f60d94a
keywords:
- WIA_DPC_EXPOSURE_METERING_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_METERING_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 518ad08cb786126c1554001f8e877418932169dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533018"
---
# <a name="wiadpcexposuremeteringmode"></a>WIA\_DPC\_暴露\_计量\_模式


WIA\_DPC\_暴露\_计量\_模式属性指定用于自动调整曝光度设置照相机的模式。

## <span id="ddk_wia_dpc_exposure_metering_mode_si"></span><span id="DDK_WIA_DPC_EXPOSURE_METERING_MODE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的常量\_DPC\_暴露\_计量\_模式属性。

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
<td><p>EXPOSUREMETERING_AVERAGE</p></td>
<td><p>设置基于整个场景的平均数的风险。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMETERING_CENTERSPOT</p></td>
<td><p>设置基于中心点的风险。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMETERING_CENTERWEIGHT</p></td>
<td><p>设置基于中心加权平均数的风险。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMETERING_MULTISPOT</p></td>
<td><p>设置基于 multispot 模式的风险。</p></td>
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

 

 





