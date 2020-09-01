---
title: KSPROPERTY \_ VIDEOCONTROL \_ CAP
description: KSPROPERTY \_ VIDEOCONTROL \_ cap 属性标识设备的视频控制功能。 必须实现此属性。
ms.assetid: 5861ae38-3253-4546-bd9f-975f98e9e3f4
keywords:
- KSPROPERTY_VIDEOCONTROL_CAPS 流媒体设备
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
ms.openlocfilehash: b9252597d5768acade6cee66ac251705df4e64d2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191251"
---
# <a name="ksproperty_videocontrol_caps"></a>KSPROPERTY \_ VIDEOCONTROL \_ CAP


KSPROPERTY \_ VIDEOCONTROL \_ cap 属性标识设备的视频控制功能。 必须实现此属性。

## <span id="ddk_ksproperty_videocontrol_caps_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_CAPS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_caps_s)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_CAPS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_caps_s)"><strong>KSPROPERTY_VIDEOCONTROL_CAPS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ VIDEOCONTROL \_ cap \_ S 结构，用于指定微型驱动程序的视频控制功能，如图像翻转或事件触发能力。

<a name="remarks"></a>注解
-------

KSPROPERTY **VideoControlCaps** \_ VIDEOCONTROL \_ Cap S 结构的 VideoControlCaps 成员 \_ 指定设备的视频控制功能。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ VIDEOCONTROL \_ CAP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_caps_s)

 

