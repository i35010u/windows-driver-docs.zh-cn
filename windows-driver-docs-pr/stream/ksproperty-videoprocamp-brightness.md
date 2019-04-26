---
title: KSPROPERTY\_VIDEOPROCAMP\_亮度
description: KSPROPERTY\_VIDEOPROCAMP\_亮度属性控制的亮度设置。 此属性为可选项。
ms.assetid: 8b099ff1-e64a-4723-9834-8a42450bebd4
keywords:
- KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS 流式处理媒体设备
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
ms.openlocfilehash: 2c0eadda61dcd7c94a235e9757678ec2c9ad5b54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327213"
---
# <a name="kspropertyvideoprocampbrightness"></a>KSPROPERTY\_VIDEOPROCAMP\_亮度


KSPROPERTY\_VIDEOPROCAMP\_亮度属性控制的亮度设置。 此属性为可选项。

## <span id="ddk_ksproperty_videoprocamp_brightness_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_BRIGHTNESS_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566089" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566089)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff566080" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566080)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的亮度设置长时间。 此值表示在过期单位数乘以 100 NTSC 源中。 对于非 NTSC 源，单位为任意的与表示消隐功能的 0 到 10000 表示纯白色。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOPROCAMP\_S 结构指定亮度。

亮度也称为是黑色的级别。 修改亮度设置，会转而为所有的亮度值同样的整个视频信号。

每个视频捕获微型驱动程序必须定义此属性的范围和默认值。 所需的范围必须是通过 +10000-10000。 默认值必须是 750 （7.5 过期）。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOPROCAMP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566089)

 

 






