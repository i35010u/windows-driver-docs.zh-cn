---
title: KSPROPERTY \_ 调谐器 \_ 输入
description: KSPROPERTY \_ 调谐器 \_ 输入属性描述当前调谐模式下的调谐器输入，例如，在电缆和天线调谐器输入之间进行选择。 必须实现此属性。
ms.assetid: b2c92531-ad1f-4152-a98d-7cae9c2c940c
keywords:
- KSPROPERTY_TUNER_INPUT 流媒体设备
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
ms.openlocfilehash: ff784bf437c69f9befd05c50f4053d3e568c43d5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107252"
---
# <a name="ksproperty_tuner_input"></a>KSPROPERTY \_ 调谐器 \_ 输入


KSPROPERTY \_ 调谐器 \_ 输入属性描述当前调谐模式下的调谐器输入，例如，在电缆和天线调谐器输入之间进行选择。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_input_ks"></span><span id="DDK_KSPROPERTY_TUNER_INPUT_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s)"><strong>KSPROPERTY_TUNER_INPUT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，它指定物理调谐器输入的数字索引。 此值应介于0到 (输入-1) 的范围内。

<a name="remarks"></a>备注
-------

KSPROPERTY 调谐器输入的结构的 **InputIndex** 成员 \_ \_ \_ 指定当前调谐器输入索引。

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

[**KSPROPERTY \_ 调谐器 \_ 输入 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s)

