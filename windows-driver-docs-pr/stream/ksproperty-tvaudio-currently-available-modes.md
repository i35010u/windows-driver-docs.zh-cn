---
title: KSPROPERTY \_ TVAUDIO \_ 当前 \_ 可用 \_ 模式
description: "\"KSPROPERTY \\_ TVAUDIO \\_ 当前 \\_ 可用 \\_ 模式\" 属性检索设备可用的电视音频模式。 必须实现此属性。"
ms.assetid: 9c98771a-7a41-469d-a441-da5c1ac5a697
keywords:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 744b6589d7bea1bb9e673827bbba31838c61154c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190391"
---
# <a name="ksproperty_tvaudio_currently_available_modes"></a>KSPROPERTY \_ TVAUDIO \_ 当前 \_ 可用 \_ 模式


"KSPROPERTY \_ TVAUDIO \_ 当前 \_ 可用 \_ 模式" 属性检索设备可用的电视音频模式。 必须实现此属性。

## <span id="ddk_ksproperty_tvaudio_currently_available_modes_ks"></span><span id="DDK_KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)"><strong>KSPROPERTY_TVAUDIO_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，它指定当前可用的电视音频模式，如立体声或 mono 音频和多语言设置。

<a name="remarks"></a>备注
-------

KSPROPERTY **Mode** \_ TVAUDIO S 结构的 Mode 成员 \_ 指定音频模式。 它包含 KS \_ TVAUDIO 模式标志的按位 \_ or \_ \* ，用于指示请求信息时设备支持的模式。

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

[**KSPROPERTY \_ TVAUDIO \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tvaudio_s)

 

