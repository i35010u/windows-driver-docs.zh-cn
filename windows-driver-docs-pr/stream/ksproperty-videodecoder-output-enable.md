---
title: KSPROPERTY\_VIDEODECODER\_OUTPUT\_启用
description: KSPROPERTY\_VIDEODECODER\_OUTPUT\_ENABLE 属性控制位于共享视频端口总线上的视频解码器的三状态输出。 此属性为可选项。
ms.assetid: 33c9a3d2-ffc0-4460-abc4-56bc83c64b55
keywords:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3ebec2f6f3816dbc7a6dc74487915c5559424eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837868"
---
# <a name="ksproperty_videodecoder_output_enable"></a>KSPROPERTY\_VIDEODECODER\_OUTPUT\_启用


KSPROPERTY\_VIDEODECODER\_OUTPUT\_ENABLE 属性控制位于共享视频端口总线上的视频解码器的三状态输出。 此属性为可选项。

## <span id="ddk_ksproperty_videodecoder_output_enable_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 ULONG，它指定三状态输出启用设置。 如果值为零，则指示三状态输出。 非零值表示设备正在积极驱动视频端口总线。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VIDEODECODER\_S 结构的**值**成员指定三个输出启用设置。

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

[**KSPROPERTY\_VIDEODECODER\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)

 

 






