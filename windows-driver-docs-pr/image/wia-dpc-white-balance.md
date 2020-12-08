---
title: WIA \_ DPC \_ 白 \_ 平衡
description: WIA \_ DPC \_ 白 \_ 平衡属性指定数字照相机如何混合颜色通道。
keywords:
- WIA_DPC_WHITE_BALANCE 图像设备
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
ms.openlocfilehash: f06db0670373b355c059b7293019412a397bf4ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808197"
---
# <a name="wia_dpc_white_balance"></a>WIA \_ DPC \_ 白 \_ 平衡


WIA \_ DPC \_ 白 \_ 平衡属性指定数字照相机如何混合颜色通道。

## <span id="ddk_wia_dpc_white_balance_si"></span><span id="DDK_WIA_DPC_WHITE_BALANCE_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 WIA \_ DPC \_ 白平衡属性的可能值 \_ ：

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
<td><p>WHITEBALANCE_AUTO</p></td>
<td><p>照相机使用自动机制来设置白平衡。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_DAYLIGHT</p></td>
<td><p>相机将白平衡设置为适合在夏令时中使用的值。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_FLASH</p></td>
<td><p>相机将白平衡设置为适用于电子闪光灯的值。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_FLORESCENT</p></td>
<td><p>相机将白平衡设置为适合与荧光灯使用的值。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_MANUAL</p></td>
<td><p>您的驱动程序可以使用 " <a href="wia-dpc-rgb-gain.md" data-raw-source="[&lt;strong&gt;WIA_DPC_RGB_GAIN&lt;/strong&gt;](wia-dpc-rgb-gain.md)"><strong>WIA_DPC_RGB_GAIN</strong></a> " 属性直接设置白平衡。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_ONEPUSH_AUTO</p></td>
<td><p>当用户按 "捕获" 按钮时，照相机会确定白色平衡设置，同时将相机指向白色表面。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_TUNGSTEN</p></td>
<td><p>相机将白平衡设置为适合与 tungsten 光源一起使用的值。</p></td>
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

## <a name="see-also"></a>请参阅


[**WIA \_ DPC \_ RGB \_ 增益**](wia-dpc-rgb-gain.md)

 

 






