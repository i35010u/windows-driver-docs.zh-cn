---
title: KSPROPERTY \_ EXTXPORT \_ 输入 \_ 信号 \_ 模式
description: KSPROPERTY \_ EXTXPORT \_ 输入 \_ 信号 \_ 模式属性设置或获取外部设备的当前输入信号模式。 例如，DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS 等。
ms.assetid: 3af5c2fb-c7dc-4dfb-b66d-fc16091fa5ad
keywords:
- KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a3edf570c5517c4fe5215b11b9eb52458742456
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106694"
---
# <a name="ksproperty_extxport_input_signal_mode"></a>KSPROPERTY \_ EXTXPORT \_ 输入 \_ 信号 \_ 模式


KSPROPERTY \_ EXTXPORT \_ 输入 \_ 信号 \_ 模式属性设置或获取外部设备的当前输入信号模式。 例如，DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS 等。

## <span id="ddk_ksproperty_extxport_input_signal_mode_ks"></span><span id="DDK_KSPROPERTY_EXTXPORT_INPUT_SIGNAL_MODE_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，用于指定外部传输的当前输入信号模式。

<a name="remarks"></a>备注
-------

KSPROPERTY **SignalMode** \_ EXTXPORT S 结构的 SignalMode 成员 \_ 指定输入信号模式。

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

[**KSPROPERTY \_ EXTXPORT \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

