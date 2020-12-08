---
title: WIA \_ IP \_ 方向
description: "\"WIA \\_ IPS \\_ 方向\" 属性描述要扫描的文档的当前方向。 WIA 微型驱动程序创建并维护此属性。"
keywords:
- WIA_IPS_ORIENTATION 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_ORIENTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f1ecf89fb0f980250a5fa171404efc2ec9439a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829941"
---
# <a name="wia_ips_orientation"></a>WIA \_ IP \_ 方向


"WIA \_ IPS \_ 方向" 属性描述要扫描的文档的当前方向。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_orientation_si"></span><span id="DDK_WIA_IPS_ORIENTATION_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

应用程序设置 WIA \_ IPS \_ 方向属性，以定义要获取的页面或图像的原始方向。 有关如何使用 WIA IPS 方向的详细 \_ 信息 \_ ，请参阅 [**wia \_ DPS \_ 页面 \_ 大小**](wia-dps-page-size.md)。

下表描述了对 WIA ip 方向有效的常量 \_ \_ 。

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
<td><p>LANSCAPE</p></td>
<td><p>方向90是逆时针旋转，相对于纵向方向。</p></td>
</tr>
<tr class="even">
<td><p>沿</p></td>
<td><p>方向为0度。</p></td>
</tr>
<tr class="odd">
<td><p>ROT180</p></td>
<td><p>方向180是逆时针旋转，相对于纵向方向。</p></td>
</tr>
<tr class="even">
<td><p>ROT270</p></td>
<td><p>方向270是逆时针旋转，相对于纵向方向。</p></td>
</tr>
</tbody>
</table>

 

"WIA \_ IPS \_ 方向" 属性描述要扫描的文档的方向。 此属性会影响当前扫描帧和可用的页面大小。

WIA \_ ip \_ ORIENTATIONis 不同于 [**wia \_ ips \_ 旋转**](wia-ips-rotation.md) 属性，这是指在扫描图像 *后* 对其应用的旋转。 因此，WIA ip 方向的 ROT180 \_ 值 \_ 不同于 wia ip 轮换的 ROT180 值 \_ \_ 。 对于 WIA \_ ip \_ 方向，ROT180 描述要扫描的物理文档的方向（相对于扫描方向）和 WIA \_ IPS \_ 旋转，ROT180 描述了在扫描图像后要应用于该图像的旋转。

"WIA \_ IPS \_ 方向" 属性对于 ADF 项是必需的，对于所有其他图像获取项则是可选的。

**注意**   如果设备的子项目不支持属性，则 WIA 服务内的兼容性层不会将对 WIA ip 方向的支持添加 \_ \_ 到从 MICROSOFT WINDOWS XP WIA 设备转换的 ADF 项。 应用程序不应预期 ADF 项将始终支持此属性，并且应始终检查是否 \_ 支持 WIA ip \_ 方向。

 

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


[**WIA \_ DPS \_ 页面 \_ 大小**](wia-dps-page-size.md)

[**WIA \_ IP \_ 轮换**](wia-ips-rotation.md)

 

 






