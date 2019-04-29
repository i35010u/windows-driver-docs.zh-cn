---
title: KSPROPERTY\_调谐器\_CAP
description: KSPROPERTY\_调谐器\_CAPS 属性描述调谐器的基本功能。 必须实现此属性。
ms.assetid: 70255053-d241-44ca-ba24-cfc442629ab3
keywords:
- KSPROPERTY_TUNER_CAPS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_CAPS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe9f65fb1c54bdb8f016cb7a8374ce350f8d2a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355850"
---
# <a name="kspropertytunercaps"></a>KSPROPERTY\_调谐器\_CAP


KSPROPERTY\_调谐器\_CAPS 属性描述调谐器的基本功能。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_caps_ks"></span><span id="DDK_KSPROPERTY_TUNER_CAPS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565828" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565828)"><strong>KSPROPERTY_TUNER_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 long 类型的值，指定流式处理的微型驱动程序支持的优化模式。

<a name="remarks"></a>备注
-------

**ModesSupported** KSPROPERTY 成员\_调谐器\_CAPS\_S 结构指示视频捕获微型驱动程序支持的优化模式。

单个优化设备可能支持优化数字电视、 模拟电视、 上午 / 调频广播，以及数字卫星系统 (DSS)。

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

[**KSPROPERTY\_TUNER\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565828)

[**KSPROPERTY\_调谐器\_模式\_CAP**](ksproperty-tuner-mode-caps.md)

 

 






