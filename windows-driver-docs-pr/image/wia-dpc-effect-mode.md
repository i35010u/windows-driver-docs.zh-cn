---
title: WIA \_ DPC \_ 效果 \_ 模式
description: WIA \_ DPC \_ 效果 \_ 模式属性指定相机的特殊图像采集模式。
keywords:
- WIA_DPC_EFFECT_MODE 图像设备
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
ms.openlocfilehash: 3da0d7ea2e9d854dab2f2857525398bfb41bfabe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818415"
---
# <a name="wia_dpc_effect_mode"></a>WIA \_ DPC \_ 效果 \_ 模式


WIA \_ DPC \_ 效果 \_ 模式属性指定相机的特殊图像采集模式。

## <span id="ddk_wia_dpc_effect_mode_si"></span><span id="DDK_WIA_DPC_EFFECT_MODE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表介绍了在 WIA \_ DPC \_ 效果模式属性中有效的常量 \_ 。

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
<td><p>EFECTMODE_BW</p></td>
<td><p>捕获灰度图像</p></td>
</tr>
<tr class="even">
<td><p>EFFECTMODE_SEPIA</p></td>
<td><p>捕获棕褐色图</p></td>
</tr>
<tr class="odd">
<td><p>EFFECTMODE_STANDARD</p></td>
<td><p>在相机的标准模式下捕获映像</p></td>
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
<td><p>在 Windows Vista 和更高版本的操作系统中已过时，不应再使用。 但是，在 Windows Vista 中仍定义此属性，以与为 Windows Server 2003、Windows XP 和 windows 的早期版本设计的应用程序和设备兼容。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





