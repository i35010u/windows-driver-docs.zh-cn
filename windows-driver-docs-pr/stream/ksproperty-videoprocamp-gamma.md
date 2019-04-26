---
title: KSPROPERTY\_VIDEOPROCAMP\_GAMMA
description: KSPROPERTY\_VIDEOPROCAMP\_GAMMA 属性控制照相机的伽玛设置。 此属性为可选项。
ms.assetid: 880f0895-6619-49ac-9753-e44b7eace83d
keywords:
- KSPROPERTY_VIDEOPROCAMP_GAMMA 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_GAMMA
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d171f8af4bcba61165f00be498599c4da6ca7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327303"
---
# <a name="kspropertyvideoprocampgamma"></a>KSPROPERTY\_VIDEOPROCAMP\_GAMMA


KSPROPERTY\_VIDEOPROCAMP\_GAMMA 属性控制照相机的伽玛设置。 此属性为可选项。

## <span id="ddk_ksproperty_videoprocamp_gamma_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_GAMMA_KS"></span>


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

 

属性值 （操作数据） 为指定照相机的伽玛设置长时间。 Gamma 乘以 100 以表示 gamma 设置的值。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOPROCAMP\_S 结构指定伽玛设置。

每个视频捕获微型驱动程序必须定义此属性的范围和默认值。 所需的范围必须是 1 和 500 之间。 默认值通常为 100 (gamma = 1) 或 220 (gamma = 2.2)，具体取决于显示中等和视频硬件。

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

 

 






