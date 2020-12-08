---
title: WIA \_ DPC \_ 数字 \_ 缩放
description: WIA \_ DPC \_ 数字 \_ 缩放属性包含数字相机获取的图像的有效缩放比例，其缩放比例为10倍。
keywords:
- WIA_DPC_DIGITAL_ZOOM 图像设备
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
ms.openlocfilehash: e52482af90beed93e095df25c0644b96d33a4dd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793603"
---
# <a name="wia_dpc_digital_zoom"></a>WIA \_ DPC \_ 数字 \_ 缩放


WIA \_ DPC \_ 数字 \_ 缩放属性包含数字相机获取的图像的有效缩放比例，其缩放比例为10倍。

## <span id="ddk_wia_dpc_digital_zoom_si"></span><span id="DDK_WIA_DPC_DIGITAL_ZOOM_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表或 wia 的 \_ 内容 \_ 范围

访问权限：读/写

<a name="remarks"></a>备注
-------

WIA \_ DPC \_ 数字 \_ 缩放值10对应于缺少数字缩放 (1x) ，这是相机捕获的标准场景大小。 值20对应于2X 缩放，其中，照相机捕获标准场景大小的四分之一。

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

 

 





