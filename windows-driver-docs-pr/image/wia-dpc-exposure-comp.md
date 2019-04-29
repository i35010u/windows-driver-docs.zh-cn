---
title: WIA\_DPC\_EXPOSURE\_COMP
description: WIA\_DPC\_暴露\_COMP 属性使您能够调整数字照相机的自动公开控件的集中点。
ms.assetid: 4b3cb013-d5fa-4f9f-9d7b-43136fab0e30
keywords:
- WIA_DPC_EXPOSURE_COMP 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_COMP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21c8a9b340f2c1d318ab253dbbf0d0acbff81965
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391755"
---
# <a name="wiadpcexposurecomp"></a>WIA\_DPC\_EXPOSURE\_COMP


WIA\_DPC\_暴露\_COMP 属性使您能够调整数字照相机的自动公开控件的集中点。

## <span id="ddk_wia_dpc_exposure_comp_si"></span><span id="DDK_WIA_DPC_EXPOSURE_COMP_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_范围或 WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

可以使用 WIA\_DPC\_暴露\_COMP 属性来调整数字照相机的自动公开控件设置点。 设置 WIA\_DPC\_暴露\_COMP 为零不会更改的出厂设置自动风险级别。

单位 WIA\_DPC\_暴露\_COMP 处于"停止"的 1000，若要允许的小数部分的停止值的比例缩放。 设置 WIA\_DPC\_暴露\_到 2000 COMP 对应于两个会更亮更多展示机会 （四次能量更多传感器上），因此图像的停止点。 设置 WIA\_DPC\_暴露\_COMP −1000 到对应于一站式小于危害 （一半的能源传感器上），因此，映像将变暗。

设置值是累加式的系统的照片公开 （顶点） 为单位。

此属性可能会表示为列表或一系列值。 只有有相应设备时，通常使用此属性[ **WIA\_DPC\_暴露\_模式**](wia-dpc-exposure-mode.md)属性设置为 EXPOSUREMODE\_手动。

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


[**WIA\_DPC\_EXPOSURE\_MODE**](wia-dpc-exposure-mode.md)

 

 






