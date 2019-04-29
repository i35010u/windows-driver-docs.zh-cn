---
title: WIA\_DPC\_RGB\_GAIN
description: WIA\_DPC\_RGB\_提升属性包含 null 终止的 Unicode 字符串，分别表示红色、 绿色和蓝色性能提升，应用到图像数据。
ms.assetid: 26448818-0885-4084-a0f3-c9e25d15dbf2
keywords:
- WIA_DPC_RGB_GAIN 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_RGB_GAIN
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a3536a8f14dd75103352bfb170d1f471603b54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392561"
---
# <a name="wiadpcrgbgain"></a>WIA\_DPC\_RGB\_GAIN


WIA\_DPC\_RGB\_提升属性包含 null 终止的 Unicode 字符串，分别表示红色、 绿色和蓝色性能提升，应用到图像数据。 例如，"4: 25:50"表示 4 较红色提升、 25，绿色提升和 50 的蓝色增益。

## <span id="ddk_wia_dpc_rgb_gain_si"></span><span id="DDK_WIA_DPC_RGB_GAIN_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE 或 WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_DPC\_RGB\_提升属性进行分析，如下所示：*R*:*G*:*B*。 *R*表示的红色提升*G*表示绿色提升，和*B*表示蓝色增益。 例如，red RGB 比率 = 4，绿色 = 2，蓝色 = 3，"4:2:3"或"2000:1000:1500"可能是 RGB 字符串。 这些值是相对于彼此。 可用于添加粒度较大的数，但颜色将相同如果红色、 绿色和蓝色的比保持不变。 此属性的值的字符串分析器应支持 UINT16 整数*R*， *G*，并*B*。

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

 

 





