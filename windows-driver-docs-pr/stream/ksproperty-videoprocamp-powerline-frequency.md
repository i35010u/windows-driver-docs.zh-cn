---
title: KSPROPERTY\_VIDEOPROCAMP\_POWERLINE\_频率
description: KSPROPERTY\_VIDEOPROCAMP\_POWERLINE\_FREQUENCY 属性指定的本地 power 行频率。 如果设备支持防闪烁处理荧光灯环境的则可能需要采用的频率。
ms.assetid: 560bb16d-2a95-408f-b32c-fa2db1c94902
keywords:
- KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10332d104e7da15be931f16887a254da65a7a539
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381926"
---
# <a name="kspropertyvideoprocamppowerlinefrequency"></a>KSPROPERTY\_VIDEOPROCAMP\_POWERLINE\_频率


KSPROPERTY\_VIDEOPROCAMP\_POWERLINE\_FREQUENCY 属性指定的本地 power 行频率。 如果设备支持防闪烁处理荧光灯环境的则可能需要采用的频率。

## <span id="ddk_ksproperty_videoprocamp_powerline_frequency_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY_KS"></span>


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

 

属性值 （操作数据） 为指定的本地 power 行频率长时间。 值表示照相机的当前电源线设置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>电源线频率控件处于禁用状态。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>电源线频率是 50 Hz。</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>电源线频率是 60 Hz。</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>电源线频率由系统自动确定。</p>
<div class="alert">
<strong>请注意</strong>  自动属性值 (3) 上不可用的所有相机 (UVC 1.1 专门)。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 set 请求时，客户端应提供在上表中的值之一**值**KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S 结构。

在 get 请求时，客户端收到的值之一前面表中**值**KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S 结构。

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

[**PowerlineFrequency 枚举**](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.PowerlineFrequency)

 

 






