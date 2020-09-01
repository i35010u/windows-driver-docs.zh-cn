---
title: KSPROPERTY \_ 波形 \_ 缓冲区
description: KSPROPERTY \_ wave \_ buffer 属性说明波形设备的缓冲区。
ms.assetid: b2ef458a-a701-4403-875b-1b06164c80a1
keywords:
- KSPROPERTY_WAVE_BUFFER 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_BUFFER
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a47c0af44029cf52626f068f20d3ce685a2b52d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192811"
---
# <a name="ksproperty_wave_buffer"></a>KSPROPERTY \_ 波形 \_ 缓冲区


KSPROPERTY \_ wave \_ buffer 属性说明波形设备的缓冲区。

## <span id="ddk_ksproperty_wave_buffer_ks"></span><span id="DDK_KSPROPERTY_WAVE_BUFFER_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer" data-raw-source="[&lt;strong&gt;KSWAVE_BUFFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer)"><strong>KSWAVE_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSWAVE \_ 缓冲区结构，用于描述缓冲区的循环属性、缓冲区大小 (以字节) 为单位，以及缓冲区的起始地址。

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

[**KSWAVE \_ 缓冲区**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer)

 

