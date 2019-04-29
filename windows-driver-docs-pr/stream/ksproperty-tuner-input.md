---
title: KSPROPERTY\_调谐器\_输入
description: KSPROPERTY\_调谐器\_输入属性描述当前优化模式下，例如电缆和天线调谐器输入之间进行选择调谐器的输入。 必须实现此属性。
ms.assetid: b2c92531-ad1f-4152-a98d-7cae9c2c940c
keywords:
- KSPROPERTY_TUNER_INPUT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_INPUT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 713d64e09f052c5e8903e070693d93cb5fb6e118
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355841"
---
# <a name="kspropertytunerinput"></a>KSPROPERTY\_调谐器\_输入


KSPROPERTY\_调谐器\_输入属性描述当前优化模式下，例如电缆和天线调谐器输入之间进行选择调谐器的输入。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_input_ks"></span><span id="DDK_KSPROPERTY_TUNER_INPUT_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565856" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565856)"><strong>KSPROPERTY_TUNER_INPUT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为的 ULONG 的指定物理调谐器输入的数字索引。 此值应为 0 到 （多个输入-1） 范围内。

<a name="remarks"></a>备注
-------

**InputIndex** KSPROPERTY 成员\_调谐器\_输入\_S 结构指定当前的调谐器输入的索引。

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

[**KSPROPERTY\_调谐器\_输入\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565856)

 

 






