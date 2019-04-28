---
title: KSPROPERTY\_时钟\_FUNCTIONTABLE
description: 客户端使用 KSPROPERTY\_时钟\_FUNCTIONTABLE 属性检索用于查询时间调度入口点\_级别，启用筛选器来执行精确速率匹配。
ms.assetid: 6dac5688-fd69-416c-a4e4-da9ccc45c32a
keywords:
- KSPROPERTY_CLOCK_FUNCTIONTABLE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_FUNCTIONTABLE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c6bacea3a80de97e5d6ac60f0f33a1177303723
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342809"
---
# <a name="kspropertyclockfunctiontable"></a>KSPROPERTY\_时钟\_FUNCTIONTABLE


客户端使用 KSPROPERTY\_时钟\_FUNCTIONTABLE 属性检索用于查询时间调度入口点\_级别，启用筛选器来执行精确速率匹配。 此属性会填写[ **KSCLOCK\_FUNCTIONTABLE** ](https://msdn.microsoft.com/library/windows/hardware/ff561020)具有函数指针时钟发布文件对象之前有效的结构。

## <span id="ddk_ksproperty_clock_functiontable_ks"></span><span id="DDK_KSPROPERTY_CLOCK_FUNCTIONTABLE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561020" data-raw-source="[&lt;strong&gt;KSCLOCK_FUNCTIONTABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561020)"><strong>KSCLOCK_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*的文件对象*发出对这些入口点的调用时，客户端提供的参数指定基础创建时钟实例时返回的文件句柄的文件对象。

*SystemTime*参数指向的位置来存储相关的系统时间。 使用此函数获取系统时间**KeQueryInterruptTime**。

另请参阅[KS 时钟](https://msdn.microsoft.com/library/windows/hardware/ff567307)。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSCLOCK\_FUNCTIONTABLE**](https://msdn.microsoft.com/library/windows/hardware/ff561020)

[**KeQueryInterruptTime**](https://msdn.microsoft.com/library/windows/hardware/ff553025)

 

 






