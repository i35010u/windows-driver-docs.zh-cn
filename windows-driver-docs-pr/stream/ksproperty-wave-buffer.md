---
title: KSPROPERTY\_波形\_缓冲区
description: KSPROPERTY\_波浪\_BUFFER 属性描述 WAVE 设备的缓冲区。
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
ms.openlocfilehash: 267b9ebb3999695eb6dbcd0c33dc7542775e7bc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823601"
---
# <a name="ksproperty_wave_buffer"></a>KSPROPERTY\_波形\_缓冲区


KSPROPERTY\_波浪\_BUFFER 属性描述 WAVE 设备的缓冲区。

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
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer" data-raw-source="[&lt;strong&gt;KSWAVE_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer)"><strong>KSWAVE_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 KSWAVE\_缓冲区结构，用于描述缓冲区的循环属性、缓冲区大小（以字节为单位）和缓冲区的起始地址。

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

[**KSWAVE\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_buffer)

 

 






