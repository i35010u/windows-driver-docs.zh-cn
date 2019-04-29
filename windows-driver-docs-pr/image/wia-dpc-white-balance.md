---
title: WIA\_DPC\_白色\_平衡
description: WIA\_DPC\_白色\_平衡属性指定数字照相机将颜色通道的融合。
ms.assetid: f0f9dd8e-940a-4a42-b6d7-1d1e86c0a530
keywords:
- WIA_DPC_WHITE_BALANCE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_WHITE_BALANCE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c425bdf3aa283ebe95db37928ce9d4dff807c0ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391707"
---
# <a name="wiadpcwhitebalance"></a>WIA\_DPC\_白色\_平衡


WIA\_DPC\_白色\_平衡属性指定数字照相机将颜色通道的融合。

## <span id="ddk_wia_dpc_white_balance_si"></span><span id="DDK_WIA_DPC_WHITE_BALANCE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

下表介绍可能的值为 WIA\_DPC\_白色\_平衡属性：

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
<td><p>WHITEBALANCE_AUTO</p></td>
<td><p>照相机使用一种自动机制来设置白平衡。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_DAYLIGHT</p></td>
<td><p>照相机设置为适合于在夏时制条件中使用的值的白平衡。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_FLASH</p></td>
<td><p>照相机设置为适合于电子 flash 中使用的值的白平衡。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_FLORESCENT</p></td>
<td><p>照相机设置为适合的荧光光源的值的白平衡。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_MANUAL</p></td>
<td><p>您的驱动程序可以直接通过使用设置白平衡<a href="wia-dpc-rgb-gain.md" data-raw-source="[&lt;strong&gt;WIA_DPC_RGB_GAIN&lt;/strong&gt;](wia-dpc-rgb-gain.md)"> <strong>WIA_DPC_RGB_GAIN</strong> </a>属性。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_ONEPUSH_AUTO</p></td>
<td><p>照相机确定白平衡设置，当用户按捕获按钮下照相机指向白色的图面时。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_TUNGSTEN</p></td>
<td><p>照相机设置为适合于与 tungsten 光源一起使用的值的白平衡。</p></td>
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

## <a name="see-also"></a>请参阅


[**WIA\_DPC\_RGB\_GAIN**](wia-dpc-rgb-gain.md)

 

 






