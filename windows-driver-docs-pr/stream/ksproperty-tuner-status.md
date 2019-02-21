---
title: KSPROPERTY\_调谐器\_状态
description: KSPROPERTY\_调谐器\_状态属性检索有关优化过程包括当前的频率的信息、 阶段锁定循环 (PLL) 偏移量和信号强度。 必须实现此属性。
ms.assetid: 8613cda2-f39b-4363-a1c7-ac91162b9fca
keywords:
- KSPROPERTY_TUNER_STATUS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 883662e0fdad11a8fdf6017605b6a986ce730a04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541277"
---
# <a name="kspropertytunerstatus"></a>KSPROPERTY\_调谐器\_状态


KSPROPERTY\_调谐器\_状态属性检索有关优化过程包括当前的频率的信息、 阶段锁定循环 (PLL) 偏移量和信号强度。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_status_ks"></span><span id="DDK_KSPROPERTY_TUNER_STATUS_KS"></span>


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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565925" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565925)"><strong>KSPROPERTY_TUNER_STATUS_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565925" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565925)"><strong>KSPROPERTY_TUNER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_调谐器\_状态\_S 结构，它指定当前的频率、 PLL 偏移量和信号强度。

<a name="remarks"></a>备注
-------

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

[**KSPROPERTY\_调谐器\_状态\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565925)

 

 






