---
title: WIA\_DPC\_FNUMBER
description: WIA\_DPC\_FNUMBER 属性与可重用的功能区，在缩放 100 f-stop 数为单位中的小孔相对应。
ms.assetid: 85f3fbc8-8b20-45a7-8ed6-0d22ac7d7f6f
keywords:
- WIA_DPC_FNUMBER 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_FNUMBER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b394e8aa8b19e451e1a404b6c0e9d3ceeb670421
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379600"
---
# <a name="wiadpcfnumber"></a>WIA\_DPC\_FNUMBER


WIA\_DPC\_FNUMBER 属性与可重用的功能区，在缩放 100 f-stop 数为单位中的小孔相对应。

## <span id="ddk_wia_dpc_fnumber_si"></span><span id="DDK_WIA_DPC_FNUMBER_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

设置 WIA\_DPC\_FNUMBER 属性是通常仅当[ **WIA\_DPC\_暴露\_模式**](wia-dpc-exposure-mode.md)属性设置为 EXPOSUREMODE\_手动或 EXPOSUREMODE\_APERTURE\_优先级。

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

 

 






