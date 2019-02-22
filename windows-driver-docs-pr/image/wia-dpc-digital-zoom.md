---
title: WIA\_DPC\_DIGITAL\_ZOOM
description: WIA\_DPC\_数字\_缩放属性包含有效的缩放比率数字照相机的获取图像的缩放因子 10。
ms.assetid: 5f1ec791-fd51-4397-ac7d-5012c020ef0a
keywords:
- WIA_DPC_DIGITAL_ZOOM 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_DIGITAL_ZOOM
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72220258d68750b6fb2c9e06d53bf51ab79e6767
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547900"
---
# <a name="wiadpcdigitalzoom"></a>WIA\_DPC\_DIGITAL\_ZOOM


WIA\_DPC\_数字\_缩放属性包含有效的缩放比率数字照相机的获取图像的缩放因子 10。

## <span id="ddk_wia_dpc_digital_zoom_si"></span><span id="DDK_WIA_DPC_DIGITAL_ZOOM_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_范围

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_DPC\_数字\_缩放值为 10 对应于数字缩放 (1 X)，这是相机捕获的标准场景大小不存在。 照相机位置捕获标准场景大小的四分之一的 2 X 缩放到对应的值为 20。

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

 

 





