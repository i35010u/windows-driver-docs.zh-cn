---
title: WIA \_ IP \_ PHOTOMETRIC \_ INTERP
description: WIA \_ IPS \_ PHOTOMETRIC \_ INTERP 属性包含白像素和黑色像素的当前设置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_PHOTOMETRIC_INTERP 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_PHOTOMETRIC_INTERP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fa86a8e32ef833b0b2e23a4ec74fb8caa92442c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839093"
---
# <a name="wia_ips_photometric_interp"></a>WIA \_ IP \_ PHOTOMETRIC \_ INTERP


WIA \_ IPS \_ PHOTOMETRIC \_ INTERP 属性包含白像素和黑色像素的当前设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_photometric_interp_si"></span><span id="DDK_WIA_IPS_PHOTOMETRIC_INTERP_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序将读取 WIA \_ ip \_ PHOTOMETRIC \_ INTERP 属性，以确定分配给白色或黑色像素 (的值，具体取决于应用程序的操作) 。

下表描述了对 WIA \_ ip PHOTOMETRIC INTERP 有效的常量 \_ \_ 。

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
<td><p>WIA_PHOTO_WHITE_0</p></td>
<td><p>白色为0，黑色为1。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PHOTO_WHITE_1</p></td>
<td><p>白色为1，黑色为0。</p></td>
</tr>
</tbody>
</table>

 

如果设备只能设置为单个值，请创建一个 WIA 的 " \_ \_ 类型"，并在其中放置有效值。

\_ \_ \_ 所有映像获取项和存储的映像都需要 WIA ip PHOTOMETRIC INTERP 属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





