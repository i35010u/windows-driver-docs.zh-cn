---
title: KSPROPERTY \_ 调谐器 \_ 模式 \_ CAP
description: KSPROPERTY \_ 调谐器 \_ mode \_ cap 属性描述支持模拟电视或无线电调谐的调谐器的优化模式功能。 必须实现此属性。
ms.assetid: 521468df-40f5-4e52-9206-127e42ad5780
keywords:
- KSPROPERTY_TUNER_MODE_CAPS 流媒体设备
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
ms.openlocfilehash: 828a53612a37e75411f5cb26bbb66ee180a9bdd4
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103544"
---
# <a name="ksproperty_tuner_mode_caps"></a>KSPROPERTY \_ 调谐器 \_ 模式 \_ CAP


KSPROPERTY \_ 调谐器 \_ mode \_ cap 属性描述支持模拟电视或无线电调谐的调谐器的优化模式功能。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_mode_caps_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_CAPS_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)"><strong>KSPROPERTY_TUNER_MODE_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，用于指定调谐器的优化功能。

<a name="remarks"></a>备注
-------

KSPROPERTY **StandardsSupported** \_ 调谐器 \_ 模式 cap 结构的 StandardsSupported 成员 \_ \_ 指定当前的模拟视频标准。

对于每个单独模式 (模拟电视、数字电视、FM、AM 或 DSS) ，微型驱动程序报告功能，例如最小和最大频率、优化粒度、结算时间和输入数。

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

[**KSPROPERTY \_ 调谐器 \_ 模式 \_ CAP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)

