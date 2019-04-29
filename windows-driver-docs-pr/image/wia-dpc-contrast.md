---
title: WIA\_DPC\_对比度
description: WIA\_DPC\_对比度属性指示捕获的映像的感知的对比度。
ms.assetid: 78477714-0cf3-464c-9d32-7aba0b7def16
keywords:
- WIA_DPC_CONTRAST 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_CONTRAST
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cba92c5e2d801629d438cec7f386cdb0dac5a1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388504"
---
# <a name="wiadpccontrast"></a>WIA\_DPC\_对比度


WIA\_DPC\_对比度属性指示捕获的映像的感知的对比度。

## <span id="ddk_wia_dpc_contrast_si"></span><span id="DDK_WIA_DPC_CONTRAST_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表或 WIA\_PROP\_范围

访问权限：读取/写入

<a name="remarks"></a>备注
-------

WIA\_DPC\_对比度属性可以包含一系列值或一系列值。

支持的最低版本值 WIA\_DPC\_对比度表示与之相反，量最少和最大值表示最大对比度。 通常情况下，中间范围表示正常，或默认的对比度值。

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

 

 





