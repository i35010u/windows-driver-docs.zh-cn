---
title: KSPROPERTY\_VIDEOCONTROL\_CAP
description: KSPROPERTY\_VIDEOCONTROL\_CAPS 属性标识设备的视频控件功能。 必须实现此属性。
ms.assetid: 5861ae38-3253-4546-bd9f-975f98e9e3f4
keywords:
- KSPROPERTY_VIDEOCONTROL_CAPS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbae7147b2f69cf8adc3fb5c2d26fcdb39b1dec6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324417"
---
# <a name="kspropertyvideocontrolcaps"></a>KSPROPERTY\_VIDEOCONTROL\_CAP


KSPROPERTY\_VIDEOCONTROL\_CAPS 属性标识设备的视频控件功能。 必须实现此属性。

## <span id="ddk_ksproperty_videocontrol_caps_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_CAPS_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566036" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566036)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566036" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566036)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_VIDEOCONTROL\_CAPS\_S 结构，它指定微型驱动程序，如翻转图像或事件触发功能的视频控件功能。

<a name="remarks"></a>备注
-------

**VideoControlCaps** KSPROPERTY 成员\_VIDEOCONTROL\_CAPS\_S 结构指定的设备的视频控件功能。

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

[**KSPROPERTY\_VIDEOCONTROL\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566036)

 

 






