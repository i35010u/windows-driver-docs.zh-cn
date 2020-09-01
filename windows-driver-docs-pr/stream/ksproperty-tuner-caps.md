---
title: KSPROPERTY \_ 调谐器 \_ CAP
description: KSPROPERTY \_ 调谐器 \_ cap 属性介绍了调谐器的基本功能。 必须实现此属性。
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
ms.openlocfilehash: 6a0dabb779993af42d4e2778f6a5b270c964a6a6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188355"
---
# <a name="ksproperty_tuner_caps"></a>KSPROPERTY \_ 调谐器 \_ CAP


KSPROPERTY \_ 调谐器 \_ cap 属性介绍了调谐器的基本功能。 必须实现此属性。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)"><strong>KSPROPERTY_TUNER_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定流式处理微型驱动程序所支持的优化模式的 LONG。

<a name="remarks"></a>备注
-------

KSPROPERTY **ModesSupported** \_ 调谐器 Cap 结构的 ModesSupported 成员 \_ \_ 指示视频捕获微型驱动程序支持的优化模式。

单个调谐设备可能支持优化数字电视、模拟电视、点/调频无线电以及数字卫星系统 (DSS) 。

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

[**KSPROPERTY \_ 调谐器 \_ CAP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)

[**KSPROPERTY \_ 调谐器 \_ 模式 \_ CAP**](ksproperty-tuner-mode-caps.md)

 

