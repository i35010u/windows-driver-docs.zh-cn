---
title: KSPROPERTY \_ VIDEOPROCAMP \_ POWERLINE \_ FREQUENCY
description: KSPROPERTY \_ VIDEOPROCAMP \_ POWERLINE \_ frequency 属性指定本地电源线频率。 如果设备支持荧光灯环境的抗闪烁处理，则可能需要此频率。
ms.assetid: 560bb16d-2a95-408f-b32c-fa2db1c94902
keywords:
- KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY 流媒体设备
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
ms.openlocfilehash: 16533e90b1d980b9a5faf618e6240d976156b304
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107362"
---
# <a name="ksproperty_videoprocamp_powerline_frequency"></a>KSPROPERTY \_ VIDEOPROCAMP \_ POWERLINE \_ FREQUENCY


KSPROPERTY \_ VIDEOPROCAMP \_ POWERLINE \_ frequency 属性指定本地电源线频率。 如果设备支持荧光灯环境的抗闪烁处理，则可能需要此频率。

## <span id="ddk_ksproperty_videoprocamp_powerline_frequency_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_POWERLINE_FREQUENCY_KS"></span>


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
<td><p>筛选器或节点</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>或<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定本地电源线频率的 LONG。 值指示照相机的当前电源线设置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>禁用了电源线频率控制。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>电源线频率为 50 Hz。</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>电源线频率为 60 Hz。</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>电源线频率由系统自动确定。</p>
<div class="alert">
<strong>注意</strong>   自动属性值 (3) 在 (UVC) 1.1 的所有相机上都不可用。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

发出集请求时，客户端应提供 KSPROPERTY VIDEOPROCAMP 节点的 **值** 成员的上一个表中的值之一 \_ \_ \_ 。

发出 get 请求时，客户端将接收 KSPROPERTY **Value** \_ VIDEOPROCAMP \_ 节点 S 结构的值成员中前一个表中的值之一 \_ 。

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

[**KSPROPERTY \_ VIDEOPROCAMP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

[**PowerlineFrequency 枚举**](/uwp/api/Windows.Media.Capture.PowerlineFrequency)

