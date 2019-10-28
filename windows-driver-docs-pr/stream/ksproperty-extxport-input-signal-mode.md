---
title: KSPROPERTY\_EXTXPORT\_输入\_信号\_模式
description: KSPROPERTY\_EXTXPORT\_输入\_信号\_模式属性设置或获取外部设备的当前输入信号模式。 例如，DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS 等。
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
ms.openlocfilehash: 4ad1ec005f0c3d8559586b14a932623a3447a87a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837952"
---
# <a name="ksproperty_extxport_input_signal_mode"></a>KSPROPERTY\_EXTXPORT\_输入\_信号\_模式


KSPROPERTY\_EXTXPORT\_输入\_信号\_模式属性设置或获取外部设备的当前输入信号模式。 例如，DV-SD/NTSC/PAL、DV-SL/NTSC/PAL、MPEG2-TS 等。

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
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，用于指定外部传输的当前输入信号模式。

<a name="remarks"></a>备注
-------

KSPROPERTY\_EXTXPORT\_S 结构的**SignalMode**成员指定输入信号模式。

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

[**KSPROPERTY\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)

 

 






