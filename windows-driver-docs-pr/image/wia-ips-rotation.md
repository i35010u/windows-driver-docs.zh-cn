---
title: WIA\_IP\_旋转
description: WIA\_IP\_旋转属性包含图像旋转的当前旋转设置，如果它实现的。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 5d117d55-b7e4-46eb-aeb5-54636749081f
keywords:
- WIA_IPS_ROTATION 成像设备
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
ms.openlocfilehash: 5f2641acc7ce0367701a9759383d74babcfe4e0c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577022"
---
# <a name="wiaipsrotation"></a>WIA\_IP\_旋转


WIA\_IP\_旋转属性包含图像旋转的当前旋转设置，如果它实现的。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_rotation_si"></span><span id="DDK_WIA_IPS_ROTATION_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

应用程序设置 WIA\_IP\_旋转属性，以通知多少 （如果在所有） 的驱动程序以将图像旋转之前驱动程序将其返回给应用程序。

下表描述了为 WIA 定义的旋转常量\_IP\_旋转。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Constant</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>纵向</p></td>
<td><p>该驱动程序将不会旋转图像。</p></td>
</tr>
<tr class="even">
<td><p>LANSCAPE</p></td>
<td><p>该驱动程序将图像旋转逆时针旋转 90 度。</p></td>
</tr>
<tr class="odd">
<td><p>ROT180</p></td>
<td><p>该驱动程序将图像旋转逆时针旋转 180 度。</p></td>
</tr>
<tr class="even">
<td><p>ROT270</p></td>
<td><p>该驱动程序将图像旋转逆时针旋转 270 度。</p></td>
</tr>
</tbody>
</table>

 

WIA 微型驱动程序负责将其发送回应用程序前旋转图像数据。 应用程序负责检查映像标头，以查看新旋转的值。

它可能很难了解当前图像的所选内容区域的旋转效果 (其定义[ **WIA\_IPS\_XPOS**](wia-ips-xpos.md)， [ **WIA\_IPS\_YPOS**](wia-ips-ypos.md)， [ **WIA\_IP\_大 XEXTENT**](wia-ips-xextent.md)，和[**WIA\_IPS\_YEXTENT** ](wia-ips-yextent.md)属性)。

*选择区域*指的从获取图像在物理扫描程序平台上的所选区域。 WIA\_IPS\_旋转属性*不*修改所选内容区域。 该驱动程序应用根据 WIA 开始沿逆时针方向旋转\_IP\_驱动程序已获得适当的选择区域后将只旋转。 WIA\_IPS\_旋转*does*影响输出图像尺寸，因此必须在生成的图像数据标头中反映这些维度。

[**WIA\_IPS\_YEXTENT** ](wia-ips-yextent.md)无关[ **WIA\_IP\_方向**](wia-ips-orientation.md)。 WIA\_IPS\_方向描述要相对于扫描的; 相反，WIA 的方向进行扫描的文档的方向\_IP\_旋转描述要应用到图像的旋转角度扫描后。

WIA\_IP\_方向可能会影响要扫描的区域。 并非所有的页大小为横向和纵向和从 WIA 中更改映像的扩展盘区中提供\_IP\_方向可以裁剪图像。 WIA\_IP\_轮换不会影响映像区和要扫描的文档的方向无关。

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

## <a name="see-also"></a>请参阅


[**WIA\_IP\_方向**](wia-ips-orientation.md)

[**WIA\_IPS\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IPS\_XPOS**](wia-ips-xpos.md)

[**WIA\_IPS\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IPS\_YPOS**](wia-ips-ypos.md)

 

 






