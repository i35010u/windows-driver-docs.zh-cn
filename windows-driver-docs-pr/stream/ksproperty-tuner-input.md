---
title: KSPROPERTY\_调谐器\_输入
description: KSPROPERTY\_调谐器\_输入属性描述当前调谐模式下的调谐器输入，例如，在电缆和天线调谐器输入之间进行选择。 必须实现此属性。
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
ms.openlocfilehash: 392e327406b8b2022468e94e1881082792128b6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837909"
---
# <a name="ksproperty_tuner_input"></a>KSPROPERTY\_调谐器\_输入


KSPROPERTY\_调谐器\_输入属性描述当前调谐模式下的调谐器输入，例如，在电缆和天线调谐器输入之间进行选择。 必须实现此属性。

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
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_INPUT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s)"><strong>KSPROPERTY_TUNER_INPUT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，指定物理调谐器输入的数字索引。 此值应介于0到（输入数1）之间。

<a name="remarks"></a>备注
-------

KSPROPERTY\_调谐器\_输入\_S 结构的**InputIndex**成员指定当前调谐器输入索引。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_调谐器\_输入\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_input_s)

 

 






