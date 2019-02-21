---
title: KSPROPERTY\_STREAM\_RATECAPABILITY
description: KSPROPERTY\_流\_RATECAPABILITY 属性允许图形管理器查询的特定流的流中涉及的所有连接点 (通过 KSPROPERTY\_PIN\_DATAROUTING) 为它们在调整到名义速率的请求的速率的能力。
ms.assetid: 73e3bf4e-2815-4890-ba12-77fbe7a7c589
keywords:
- KSPROPERTY_STREAM_RATECAPABILITY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_RATECAPABILITY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77dbfcd29ae981c4efafcb89c466b7139241c32b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540769"
---
# <a name="kspropertystreamratecapability"></a>KSPROPERTY\_STREAM\_RATECAPABILITY


KSPROPERTY\_流\_RATECAPABILITY 属性允许图形管理器查询的特定流的流中涉及的所有连接点 (通过 KSPROPERTY\_PIN\_DATAROUTING) 为它们在调整到名义速率的请求的速率的能力。

## <span id="ddk_ksproperty_stream_ratecapability_ks"></span><span id="DDK_KSPROPERTY_STREAM_RATECAPABILITY_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566752" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566752)"><strong>KSRATE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566754" data-raw-source="[&lt;strong&gt;KSRATE_CAPABILITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566754)"><strong>KSRATE_CAPABILITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY\_流\_应实现 RATECAPABILITY，如果 pin 允许速率更改或拓扑结构上相关的插针之间的接口不同，导致使用了不同的时间戳格式。 此外可以使用属性将时间戳格式一般情况下，如跳下降请求。

修改的数据来重新采样速率的 pin 支持该属性或时间戳更改。 所有速率更改都涉及请求速率和确定多少特定 pin 可以更正该速率，若要获取的名义 1.0 速率。 例如，pin 请求 2.0 视频的播放速率意味着呈现两次的名义率的视频剪辑; 的请求0.5 的速率请求暗示一半速度呈现。

费率请求包含演示文稿开始时间和该速率请求的持续时间。 这样可能适用于数据流要考虑的特定部分的约束。 呈现时间，分子/分母对和持续时间单位以表示指定结构中的接口。 如果未使用的标准接口，无法 pin 发送初始速率更改查询。

Pin 必须能够接受接口标识符使用的任何 pin 类似的拓扑。 它还必须将转换为其自己的相应值的接口标识符和时间单位。 以这种方式，客户端可以从一个已知的接口点遍历图形并且具有单位转换每个步骤的方式连接点。

务必要支持此属性，如果接口更改即使率不能进行更改，这样该接口，并进行查询时，可以调整时间单位。 结果可能不会更改返回的速率，但接口、 PresentationStart 和持续时间将会更改。

速率功能请求仅在暂停或运行状态下执行，并将更改为任何其他状态后变为无效。 因为它们通常是只是请求将时间戳格式，应始终成功的查询速率最初是 1.0。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSRATE**](https://msdn.microsoft.com/library/windows/hardware/ff566752)

[**KSRATE\_CAPABILITY**](https://msdn.microsoft.com/library/windows/hardware/ff566754)

 

 






