---
title: WIA \_ IP \_ 轮换
description: '\_ \_ 如果已实现，WIA IPS 旋转属性包含图像旋转的当前旋转设置。 WIA 微型驱动程序创建并维护此属性。'
keywords:
- WIA_IPS_ROTATION 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ROTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42b070234f9fdb468902ff5899e3d7e42ee37ac5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783205"
---
# <a name="wia_ips_rotation"></a>WIA \_ IP \_ 轮换


\_ \_ 如果已实现，WIA IPS 旋转属性包含图像旋转的当前旋转设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_rotation_si"></span><span id="DDK_WIA_IPS_ROTATION_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序设置 WIA \_ IPS \_ 旋转属性，以便在驱动程序将图像返回到应用程序之前，如果所有) 都要旋转图像，则通知驱动程序 (量。

下表介绍为 WIA ip 轮换定义的旋转常量 \_ \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回的常量</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>沿</p></td>
<td><p>驱动程序将不会旋转图像。</p></td>
</tr>
<tr class="even">
<td><p>LANSCAPE</p></td>
<td><p>驱动程序逆时针旋转图像90度。</p></td>
</tr>
<tr class="odd">
<td><p>ROT180</p></td>
<td><p>驱动程序逆时针旋转图像180度。</p></td>
</tr>
<tr class="even">
<td><p>ROT270</p></td>
<td><p>驱动程序逆时针旋转图像270度。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序负责旋转图像数据，然后再将其发送回应用程序。 应用程序负责检查图像标头以查看新旋转的值。

由于 [**wia \_ ips \_ XPOS**](wia-ips-xpos.md)、 [**wia \_ ip \_ YPOS**](wia-ips-ypos.md)、 [**wia \_ ips \_ XEXTENT**](wia-ips-xextent.md)和 [**wia \_ ip \_ YEXTENT**](wia-ips-yextent.md) 属性) 定义的，因此，可能很难了解当前图像选择区域的旋转效果 (。

*选择区域* 指的是物理扫描仪平台上从其获取图像的选定区域。 WIA \_ ip \_ 轮换属性不会 *not* 修改选择区域。 \_ \_ 仅当驱动程序获得了适当的选择区域后，该驱动程序才会根据 WIA IPS 旋转应用逆时针旋转。 WIA \_ ip \_ 轮换 *确实* 会影响输出图像的尺寸，因此这些维度必须反映在生成的映像的数据标头中。

[**WIA \_IPS \_ YEXTENT**](wia-ips-yextent.md) 与 [**WIA \_ ip \_ 方向**](wia-ips-orientation.md)无关。 WIA \_ ips \_ 方向说明了相对于扫描方向要扫描的文档方向; 相反，wia \_ ips \_ 旋转描述了在扫描图像后要应用于该图像的旋转。

WIA \_ ip \_ 方向可能会影响要扫描的区域。 并非所有页面大小都在横向和纵向都可用，因此，来自 WIA IPS 方向的更改中的图像 \_ 范围 \_ 可能会裁剪映像。 WIA \_ ip \_ 轮换不会影响图像区，并且与要扫描的文档的方向无关。

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

## <a name="see-also"></a>请参阅


[**WIA \_ IP \_ 方向**](wia-ips-orientation.md)

[**WIA \_ IP \_ XEXTENT**](wia-ips-xextent.md)

[**WIA \_ IP \_ XPOS**](wia-ips-xpos.md)

[**WIA \_ IP \_ YEXTENT**](wia-ips-yextent.md)

[**WIA \_ IP \_ YPOS**](wia-ips-ypos.md)

 

 






