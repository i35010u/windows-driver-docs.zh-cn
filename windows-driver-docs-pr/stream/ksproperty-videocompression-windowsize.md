---
title: KSPROPERTY\_VIDEOCOMPRESSION\_窗口大小
description: KSPROPERTY\_VIDEOCOMPRESSION\_窗口大小属性控制描述平均帧大小的数据速率。 必须实现此属性。
ms.assetid: 44cf4bb6-7ddb-4a72-8a77-7dc390aa8c12
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE 流式处理媒体设备
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
ms.openlocfilehash: ebaed8b3800ebfced36a6a55daee4815f228cbcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382008"
---
# <a name="kspropertyvideocompressionwindowsize"></a>KSPROPERTY\_VIDEOCOMPRESSION\_窗口大小


KSPROPERTY\_VIDEOCOMPRESSION\_窗口大小属性控制描述平均帧大小的数据速率。 必须实现此属性。

## <span id="ddk_ksproperty_videocompression_windowsize_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE_KS"></span>


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
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为 long 类型的值，指定表示平均帧大小的数据速率。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOCOMPRESSION\_S 结构指定的窗口大小。

微型驱动程序支持此属性应设置**KS\_CompressionCaps\_CanWindow**标记中**功能**隶属[ **KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)检索微型驱动程序的视频的压缩功能的结构。 如果微型驱动程序设置**KS\_CompressionCaps\_CanWindow**标志，它应提供 get 和 set 支持的属性。

大小的窗口*n，* 平均帧大小的任何连续*n*帧不能超过流的指定的数据速率，尽管*单个*的框架可能更大或更小。 例如，如果已设置为 150 千字节 / 秒 (KBps) 第二个 (fps) 电影，每 15 帧上的数据速率*平均*小于或等于 10 千字节为单位，因此必须为每个帧的大小。 只要 （跨计算 15 每秒帧数的电影） 的平均大小小于或等于 10 千字节为单位，单个帧可能更大或更小。

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

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 






