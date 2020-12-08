---
title: KSPROPERTY \_ VIDEOCOMPRESSION \_ WINDOWSIZE
description: KSPROPERTY \_ VIDEOCOMPRESSION \_ WINDOWSIZE 属性控制描述平均帧大小的数据速率。 必须实现此属性。
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb3ae946b89fff713c19be17784bd2587a2a7f98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840861"
---
# <a name="ksproperty_videocompression_windowsize"></a>KSPROPERTY \_ VIDEOCOMPRESSION \_ WINDOWSIZE


KSPROPERTY \_ VIDEOCOMPRESSION \_ WINDOWSIZE 属性控制描述平均帧大小的数据速率。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_windowsize_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE_KS"></span>


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
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 LONG，用于指定表示平均帧大小的数据速率。

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ VIDEOCOMPRESSION S 结构的 Value 成员 \_ 指定窗口大小。

支持此属性的微型驱动程序应在用于检索 VIDEOCOMPRESSION 视频压缩功能的 [**KSPROPERTY \_ GETINFO \_ 微型驱动程序 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)结构的 "**功能**" 成员中设置 **KS \_ CompressionCaps \_ CanWindow** 标志。 如果微型驱动程序设置了 **KS \_ CompressionCaps \_ CanWindow** 标志，则它应同时提供对属性的 get 和 set 支持。

对于大小为 n 的窗口 *，* 任何连续 *n* 帧的平均帧大小不得超过流的指定数据速率，尽管 *各个* 帧可能更大或更小。 例如，如果已将数据速率设置为每秒 150 kb (KBps) 每秒15帧 (fps) 电影，则每个帧的 *平均* 大小必须小于或等于 10 kb。 只需在影片) 的每秒15帧之间计算 (每秒15帧就会小于或等于 10 kb，单独帧越大或更小。

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

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

