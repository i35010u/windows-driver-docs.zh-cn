---
title: WIA\_IPS\_PHOTOMETRIC\_INTERP
description: WIA\_IPS\_PHOTOMETRIC\_INTERP 属性包含白色和黑色像素为单位的当前设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 5d48ec37-68bb-446a-9236-c88d26f8a549
keywords:
- WIA_IPS_PHOTOMETRIC_INTERP 成像设备
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
ms.openlocfilehash: 3ef34df6b44809f83bd295604f7161d9122b49bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383685"
---
# <a name="wiaipsphotometricinterp"></a>WIA\_IPS\_PHOTOMETRIC\_INTERP


WIA\_IPS\_PHOTOMETRIC\_INTERP 属性包含白色和黑色像素为单位的当前设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_photometric_interp_si"></span><span id="DDK_WIA_IPS_PHOTOMETRIC_INTERP_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_IPS\_PHOTOMETRIC\_INTERP 属性来确定分配给白色或黑色像素 （具体取决于应用程序的作用） 的值。

下表描述了有效使用 WIA 的常量\_IPS\_PHOTOMETRIC\_INTERP.

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
<td><p>WIA_PHOTO_WHITE_0</p></td>
<td><p>白色为 0，并且黑色为 1。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PHOTO_WHITE_1</p></td>
<td><p>空白是 1，并且黑色是 0。</p></td>
</tr>
</tbody>
</table>

 

如果设备可以设置为单个值，创建 WIA\_PROP\_列表类型，并将有效的值放入其中。

WIA\_IPS\_PHOTOMETRIC\_INTERP 属性是必需的所有图像采集项和存储的图像。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





