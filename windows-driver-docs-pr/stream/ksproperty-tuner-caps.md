---
title: KSPROPERTY\_调谐器\_CAP
description: KSPROPERTY\_调谐器\_CAP 属性介绍了调谐器的基本功能。 必须实现此属性。
ms.assetid: 70255053-d241-44ca-ba24-cfc442629ab3
keywords:
- KSPROPERTY_TUNER_CAPS 流媒体设备
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
ms.openlocfilehash: 21d1bb6509b12196f41570936522165a65b21338
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837920"
---
# <a name="ksproperty_tuner_caps"></a>KSPROPERTY\_调谐器\_CAP


KSPROPERTY\_调谐器\_CAP 属性介绍了调谐器的基本功能。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_caps_ks"></span><span id="DDK_KSPROPERTY_TUNER_CAPS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)"><strong>KSPROPERTY_TUNER_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定流式处理微型驱动程序支持的优化模式的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY\_调谐器\_CAP\_S 结构的 " **ModesSupported** " 成员指示视频捕获微型驱动程序支持的优化模式。

单个调谐设备可能支持优化数字电视、模拟电视、点/调频无线电以及数字卫星系统（DSS）。

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

[**KSPROPERTY\_调谐器\_CAP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)

[**KSPROPERTY\_调谐器\_模式\_CAP**](ksproperty-tuner-mode-caps.md)

 

 






