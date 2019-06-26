---
title: KSPROPERTY\_VIDEOPROCAMP\_饱和度
description: KSPROPERTY\_VIDEOPROCAMP\_饱和度属性控制照相机的饱和度或色度提升设置。 此属性为可选项。
ms.assetid: 1b7fd731-088b-4370-a537-9e302d28864b
keywords:
- KSPROPERTY_VIDEOPROCAMP_SATURATION 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_SATURATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72dd24d7e03064cce06d95c9768af0605c34b211
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381922"
---
# <a name="kspropertyvideoprocampsaturation"></a>KSPROPERTY\_VIDEOPROCAMP\_饱和度


KSPROPERTY\_VIDEOPROCAMP\_饱和度属性控制照相机的饱和度或色度提升设置。 此属性为可选项。

## <span id="ddk_ksproperty_videoprocamp_saturation_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_SATURATION_KS"></span>


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
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的饱和度设置长时间。 饱和度设置的值表示为提升乘以 100。

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_VIDEOPROCAMP\_S 结构指定饱和度设置。

每个视频捕获微型驱动程序必须定义此属性的范围和默认值。 所需的范围必须是 0 到 10000。 默认值必须是 100 (1 x)。

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

[**KSPROPERTY\_VIDEOPROCAMP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 






