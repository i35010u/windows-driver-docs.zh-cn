---
title: KSPROPERTY\_时钟\_FUNCTIONTABLE
description: 客户端使用 KSPROPERTY\_时钟\_FUNCTIONTABLE 属性来检索在调度\_级别查询时间的入口点，这使筛选器能够执行精确的速率匹配。
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
ms.openlocfilehash: b15fe10a798fb8b19e56f4c83036238d353c2506
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826900"
---
# <a name="ksproperty_clock_functiontable"></a>KSPROPERTY\_时钟\_FUNCTIONTABLE


客户端使用 KSPROPERTY\_时钟\_FUNCTIONTABLE 属性来检索在调度\_级别查询时间的入口点，这使筛选器能够执行精确的速率匹配。 此属性使用有效的函数指针填充[**KSCLOCK\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)结构，直到时钟的文件对象发布。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable" data-raw-source="[&lt;strong&gt;KSCLOCK_FUNCTIONTABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)"><strong>KSCLOCK_FUNCTIONTABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当客户端调用这些入口点时，客户端提供的*FileObject*参数指定创建时钟实例时返回的文件句柄基础的文件对象。

*SystemTime*参数指向用于存储关联系统时间的位置。 使用函数**KeQueryInterruptTime**获取系统时间。

另请参阅[KS 时钟](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSCLOCK\_FUNCTIONTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksclock_functiontable)

[**KeQueryInterruptTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryinterrupttime)

 

 






