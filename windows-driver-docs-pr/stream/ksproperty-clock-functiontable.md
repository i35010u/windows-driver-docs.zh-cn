---
title: KSPROPERTY \_ 时钟 \_ FUNCTIONTABLE
description: 客户端使用 KSPROPERTY \_ 时钟 \_ FUNCTIONTABLE 属性来检索在调度级别查询时间的入口点 \_ ，这使筛选器能够执行精确速率匹配。
ms.assetid: 6dac5688-fd69-416c-a4e4-da9ccc45c32a
keywords:
- KSPROPERTY_CLOCK_FUNCTIONTABLE 流媒体设备
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
ms.openlocfilehash: b8e5b82f2982ad544a48c86cd6cb7e1e1d2b1025
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107122"
---
# <a name="ksproperty_clock_functiontable"></a>KSPROPERTY \_ 时钟 \_ FUNCTIONTABLE


客户端使用 KSPROPERTY \_ 时钟 \_ FUNCTIONTABLE 属性来检索在调度级别查询时间的入口点 \_ ，这使筛选器能够执行精确速率匹配。 此属性使用有效的函数指针填充 [**KSCLOCK \_ FUNCTIONTABLE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable) 结构，直到时钟的文件对象被释放。

## <span id="ddk_ksproperty_clock_functiontable_ks"></span><span id="DDK_KSPROPERTY_CLOCK_FUNCTIONTABLE_KS"></span>


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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable" data-raw-source="[&lt;strong&gt;KSCLOCK_FUNCTIONTABLE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)"><strong>KSCLOCK_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当客户端调用这些入口点时，客户端提供的 *FileObject* 参数指定创建时钟实例时返回的文件句柄基础的文件对象。

*SystemTime*参数指向用于存储关联系统时间的位置。 使用函数 **KeQueryInterruptTime**获取系统时间。

另请参阅 [KS 时钟](./ks-clocks.md)。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSCLOCK \_ FUNCTIONTABLE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)

[**KeQueryInterruptTime**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryinterrupttime)

