---
title: KSPROPERTY \_ VIDEOCONTROL \_ 模式
description: KSPROPERTY \_ VIDEOCONTROL \_ mode 属性控制映像生产的模式。 这包括用于水平和垂直图像翻转的设置，以及通过外部触发器启用帧捕获。 此属性是可选的。
ms.assetid: b101b348-cfd4-46a1-857a-9e7cb3f35ce5
keywords:
- KSPROPERTY_VIDEOCONTROL_MODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCONTROL_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2b309a19d0a8f9081d18553a413796f4f145d0c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189959"
---
# <a name="ksproperty_videocontrol_mode"></a>KSPROPERTY \_ VIDEOCONTROL \_ 模式


KSPROPERTY \_ VIDEOCONTROL \_ mode 属性控制映像生产的模式。 这包括用于水平和垂直图像翻转的设置，以及通过外部触发器启用帧捕获。 此属性是可选的。

## <span id="ddk_ksproperty_videocontrol_mode_ks"></span><span id="DDK_KSPROPERTY_VIDEOCONTROL_MODE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)"><strong>KSPROPERTY_VIDEOCONTROL_MODE_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCONTROL_MODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)"><strong>KSPROPERTY_VIDEOCONTROL_MODE_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ VIDEOCONTROL \_ cap \_ S 结构，用于指定微型驱动程序的视频控制功能，如图像翻转或事件触发能力。

<a name="remarks"></a>备注
-------

KSPROPERTY **Mode** \_ VIDEOCONTROL \_ 模式 S 结构的 mode 成员 \_ 指定视频控制模式。

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

[**KSPROPERTY \_ VIDEOCONTROL \_ 模式 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocontrol_mode_s)

 

