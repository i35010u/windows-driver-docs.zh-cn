---
title: KSPROPERTY\_VIDEOPROCAMP\_背景光\_补偿
description: KSPROPERTY\_VIDEOPROCAMP\_背景光\_补偿属性控制在照像机上的后 light 补偿设置。 此属性为可选项。
ms.assetid: d893fc01-048a-4f2e-8587-d71be0796dcc
keywords:
- KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dd8ce1f0b2cda9a45a2373140c721ac739f3e16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540592"
---
# <a name="kspropertyvideoprocampbacklightcompensation"></a>KSPROPERTY\_VIDEOPROCAMP\_背景光\_补偿


KSPROPERTY\_VIDEOPROCAMP\_背景光\_补偿属性控制在照像机上的后 light 补偿设置。 此属性为可选项。

## <span id="ddk_ksproperty_videoprocamp_backlight_compensation_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_BACKLIGHT_COMPENSATION_KS"></span>


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

 

属性值 （操作数据） 为指定照相机的后 light 补偿设置长时间。 此值可能为 0 或 1。 此属性的默认值为 1。 值为 0 指示，禁用后 light 补偿。 默认值为 1 指示启用后 light 补偿。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOPROCAMP\_S 结构指定是启用还是禁用背景光补偿。

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

 

 






