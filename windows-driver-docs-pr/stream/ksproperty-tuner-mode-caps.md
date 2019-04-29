---
title: KSPROPERTY\_调谐器\_模式\_CAP
description: KSPROPERTY\_调谐器\_模式\_CAPS 属性描述的调试支持模拟电视调谐器的模式和单选优化功能。 必须实现此属性。
ms.assetid: 521468df-40f5-4e52-9206-127e42ad5780
keywords:
- KSPROPERTY_TUNER_MODE_CAPS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_MODE_CAPS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a3e709a4eca0e4433fb29dbfc2a5e11107b13c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378905"
---
# <a name="kspropertytunermodecaps"></a>KSPROPERTY\_调谐器\_模式\_CAP


KSPROPERTY\_调谐器\_模式\_CAPS 属性描述的调试支持模拟电视调谐器的模式和单选优化功能。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_mode_caps_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_CAPS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565872" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565872)"><strong>KSPROPERTY_TUNER_MODE_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 ULONG 指定调谐器的优化功能。

<a name="remarks"></a>备注
-------

**StandardsSupported** KSPROPERTY 成员\_调谐器\_模式\_CAPS\_S 结构指定的当前模拟视频标准。

为每个单独的模式 (模拟电视、 数字电视、 FM、 AM、 或 DSS)、 微型驱动程序报告功能，例如最小和最大频率、 优化的粒度，确定时间、 和数字的输入。

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

[**KSPROPERTY\_调谐器\_模式\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565872)

 

 






