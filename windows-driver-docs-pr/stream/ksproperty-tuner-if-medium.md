---
title: KSPROPERTY \_ 调谐器 \_ IF \_ 中型
description: '\_ \_ 如果 \_ 介质为支持数字电视调谐的设备描述了中间频率引脚介质，则 KSPROPERTY 调谐器。 此属性是可选的。'
ms.assetid: 1144777c-e81c-4b8f-a634-411591c71356
keywords:
- KSPROPERTY_TUNER_IF_MEDIUM 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_IF_MEDIUM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36c2a80355ed7fa55e6392351b9f651fd9488fcb
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104556"
---
# <a name="ksproperty_tuner_if_medium"></a>KSPROPERTY \_ 调谐器 \_ IF \_ 中型


\_ \_ 如果 \_ 介质为支持数字电视调谐的设备描述了中间频率引脚介质，则 KSPROPERTY 调谐器。 此属性是可选的。

## <span id="ddk_ksproperty_tuner_if_medium_ks"></span><span id="DDK_KSPROPERTY_TUNER_IF_MEDIUM_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s)"><strong>KSPROPERTY_TUNER_IF_MEDIUM_S</strong></a></p></td>
<td><p><a href="/previous-versions/ff563538(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](/previous-versions/ff563538(v=vs.85))"><strong>KSPIN_MEDIUM</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPIN \_ 中型结构，该结构为能够支持优化到中间频率的 pin 指定中型 GUID。

<a name="remarks"></a>注解
-------

**IFMedium** \_ \_ 如果 \_ MEDIUM \_ S 结构指定中间频率 pin 的中等 GUID，则为 KSPROPERTY 调谐器的 IFMedium 成员。

如果视频捕获微型驱动程序支持 KSPROPERTY \_ 调谐器 \_ ，若为 \_ MEDIUM，则 *kstvtune.ax* 会创建一个附加的 pin，用于表示位于调谐器上的基于硬件的 mpeg-2 传输流。 此 pin 仅用于定义关系图拓扑。 从 *kstvtune.ax* 上的此插针流向用户模式流的数据样本包含 [**KS \_ TVTUNER \_ 更改 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_tvtuner_change_info) 结构。

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

[**KSPROPERTY \_ 调谐器（ \_ 如果为 \_ MEDIUM \_ ）**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s)

