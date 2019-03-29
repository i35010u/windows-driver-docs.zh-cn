---
title: KSPROPERTY\_VIDEOCONTROL\_帧\_费率
description: KSPROPERTY\_VIDEOCONTROL\_帧\_费率属性枚举可用的帧速率。 此属性为可选项。
ms.assetid: f2b6fabc-c03b-4fa5-9e5b-43d7a1c26578
keywords:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11a26829f683dfda9d0fa6d72a324944c3c5c4f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566904"
---
# <a name="kspropertyvideocontrolframerates"></a>KSPROPERTY\_VIDEOCONTROL\_帧\_费率


KSPROPERTY\_VIDEOCONTROL\_帧\_费率属性枚举可用的帧速率。 此属性为可选项。

## <span id="ddk_ksproperty_videocontrol_frame_rates_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_FRAME_RATES_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
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
<td><p>Filter</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566041" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566041)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563441" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563441)"><strong>KSMULTIPLE_ITEM</strong> </a>数组</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSMULTIPLE\_项数组，其中介绍了可用的帧速率以 100 毫微秒为单位。

<a name="remarks"></a>备注
-------

KSMULTIPLE 中返回可用的帧速率\_项数组。 应用程序发送微型驱动程序 KSPROPERTY\_VIDEOCONTROL\_帧\_KSPROPERTY 中指定的流索引和图像尺寸的费率请求\_VIDEOCONTROL\_帧\_费率\_S 结构。 微型驱动程序返回调用方的 KSMULTIPLE 中的帧速率信息\_项数组缓冲区。 此缓冲区已固定的标头 (KSMULTIPLE\_项)，以及可变长度数据量的后面 (KSMULTIPLE 中值为基础的\_项结构)。

每个值是 100 nansecond 增量。

如果缓冲区的大小传递给微型驱动程序为零，微型驱动程序应设置**NumberOfBytesToTransfer**成员的 HW\_流\_请求\_块结构传递给所需的缓冲区大小的微型驱动程序，并返回状态\_缓冲区\_溢出。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCONTROL\_FRAME\_RATES\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566041)

 

 






