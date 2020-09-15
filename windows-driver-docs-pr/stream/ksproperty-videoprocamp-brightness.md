---
title: KSPROPERTY \_ VIDEOPROCAMP \_ 亮度
description: KSPROPERTY \_ VIDEOPROCAMP \_ 亮度属性控制亮度设置。 此属性是可选的。
ms.assetid: 8b099ff1-e64a-4723-9834-8a42450bebd4
keywords:
- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1935378927a76833b296ff3602705afd8a60ee73
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103022"
---
# <a name="ksproperty_videoprocamp_brightness"></a>KSPROPERTY \_ VIDEOPROCAMP \_ 亮度


KSPROPERTY \_ VIDEOPROCAMP \_ 亮度属性控制亮度设置。 此属性是可选的。

## <span id="ddk_ksproperty_videoprocamp_brightness_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>或<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定相机亮度设置的 LONG 值。 对于 NTSC 源，此值以 PROTOKOL 单位乘以100。 对于非 NTSC 源，单位为任意，0表示消隐，10000表示纯白色。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOPROCAMP S 结构的值成员 \_ 指定亮度。

亮度也称为黑色。 修改亮度设置将为所有亮度值平均移动整个视频信号。

每个视频捕获微型驱动程序都必须为此属性定义一个范围和默认值。 所需范围必须为-10000 到 + 10000。 默认值必须是 750 (7.5 PROTOKOL) 。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOPROCAMP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

