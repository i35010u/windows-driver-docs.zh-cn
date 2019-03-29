---
title: WIA\_DPC\_暴露\_时间
description: WIA\_DPC\_暴露\_时间属性对应于快门速度，以秒为单位，按 10,000 缩放。
ms.assetid: 78f12aaa-4b7b-4ba3-a6af-791e97581d26
keywords:
- WIA_DPC_EXPOSURE_TIME 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63bd9173546332a2e795d2d7f79aea59d0c27f50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576259"
---
# <a name="wiadpcexposuretime"></a>WIA\_DPC\_暴露\_时间


WIA\_DPC\_暴露\_时间属性对应于快门速度，以秒为单位，按 10,000 缩放。

## <span id="ddk_wia_dpc_exposure_time_si"></span><span id="DDK_WIA_DPC_EXPOSURE_TIME_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_范围或 WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

通常情况下，设备使用 WIA\_DPC\_暴露\_时间属性时，才[ **WIA\_DPC\_暴露\_模式**](wia-dpc-exposure-mode.md)属性设置为 EXPOSUREMODE\_手动或 EXPOSUREMODE\_快门\_优先级。

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
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_DPC\_EXPOSURE\_MODE**](wia-dpc-exposure-mode.md)

 

 






