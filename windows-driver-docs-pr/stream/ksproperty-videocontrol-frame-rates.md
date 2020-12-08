---
title: KSPROPERTY \_ VIDEOCONTROL \_ 帧 \_ 速率
description: "\"KSPROPERTY \\_ VIDEOCONTROL \\_ 帧 \\_ 速率\" 属性枚举可用的帧速率。 此属性是可选的。"
keywords:
- KSPROPERTY_VIDEOCONTROL_FRAME_RATES 流媒体设备
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
ms.openlocfilehash: 52ec2bdfc83834b92274b57cae1cfaf03205053a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836631"
---
# <a name="ksproperty_videocontrol_frame_rates"></a>KSPROPERTY \_ VIDEOCONTROL \_ 帧 \_ 速率


"KSPROPERTY \_ VIDEOCONTROL \_ 帧 \_ 速率" 属性枚举可用的帧速率。 此属性是可选的。

## <span id="ddk_ksproperty_videocontrol_frame_rates_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_FRAME_RATES_KS"></span>


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
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)"><strong>KSPROPERTY_VIDEOCONTROL_FRAME_RATES_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a> 数组</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSMULTIPLE \_ 项数组，描述以100毫微秒为单位的可用帧速率。

<a name="remarks"></a>备注
-------

可用帧速率在 KSMULTIPLE 项数组中返回 \_ 。 应用程序向微型驱动程序发送 KSPROPERTY \_ VIDEOCONTROL \_ 帧 \_ 速率请求，以指定 KSPROPERTY \_ VIDEOCONTROL \_ 帧 \_ 速率 \_ S 结构中的流索引和图像维度。 微型驱动程序返回调用方的 KSMULTIPLE 项数组缓冲区中的帧速率信息 \_ 。 此缓冲区具有固定的标头 (KSMULTIPLE \_ 项) ，并根据 KSMULTIPLE \_ 项结构) 中的值 (其后面的可变长度数据量。

单个值为 100-nansecond 增量。

如果传递给微型驱动程序的缓冲区大小为零，则微型驱动程序应将 **NumberOfBytesToTransfer** \_ 传递给微型驱动程序的 HW 流请求块结构的 NumberOfBytesToTransfer 成员设置 \_ \_ 为所需的缓冲区大小并返回状态 \_ 缓冲区 \_ 溢出。

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

[**KSPROPERTY \_ VIDEOCONTROL \_ 帧 \_ 速率 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_frame_rates_s)

