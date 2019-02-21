---
title: KSPROPERTY\_VIDEOPROCAMP\_对比度
description: KSPROPERTY\_VIDEOPROCAMP\_对比度属性控制照相机的对比度 （亮度收益） 设置。 此属性为可选项。
ms.assetid: 0e94aec4-b258-44be-aa6e-f0a40b803564
keywords:
- KSPROPERTY_VIDEOPROCAMP_CONTRAST 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_CONTRAST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 812a70a0fe49a6998b292f5eadc9cf3dcbb22fa6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540835"
---
# <a name="kspropertyvideoprocampcontrast"></a>KSPROPERTY\_VIDEOPROCAMP\_对比度


KSPROPERTY\_VIDEOPROCAMP\_对比度属性控制照相机的对比度 （亮度收益） 设置。 此属性为可选项。

## <span id="ddk_ksproperty_videoprocamp_contrast_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_CONTRAST_KS"></span>


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

 

属性值 （操作数据） 为 long 类型的值，指定照相机的对比度设置。 对比度值表示为提升系数乘以 100。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOPROCAMP\_S 结构指定的对比度值。

每个视频捕获微型驱动程序必须定义的范围和默认值**值**此属性的成员。 所需的范围必须是 0 到 10000。 默认值必须是 100 (1 x)。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOPROCAMP\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566089)

 

 






