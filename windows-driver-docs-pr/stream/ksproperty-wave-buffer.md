---
title: KSPROPERTY \_ 波形 \_ 缓冲区
description: KSPROPERTY \_ wave \_ buffer 属性说明波形设备的缓冲区。
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
ms.openlocfilehash: c7f265086c70fa3b0fd2b122d4c02da996e8ea1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830830"
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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer" data-raw-source="[&lt;strong&gt;KSWAVE_BUFFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer)"><strong>KSWAVE_BUFFER</strong></a></p></td>
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

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSWAVE \_ 缓冲区**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer)

