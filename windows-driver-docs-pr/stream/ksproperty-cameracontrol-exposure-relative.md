---
title: KSPROPERTY \_ CAMERACONTROL \_ 曝光 \_ 相对
description: KSPROPERTY \_ CAMERACONTROL \_ 曝露 \_ 相对属性指定电子快门速度。
ms.assetid: a4003fcd-9dc8-4889-9ce0-e4f09273d152
keywords:
- KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d31de74841b2bb0b01868762d942a1c16b55509
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186593"
---
# <a name="ksproperty_cameracontrol_exposure_relative"></a>KSPROPERTY \_ CAMERACONTROL \_ 曝光 \_ 相对


KSPROPERTY \_ CAMERACONTROL \_ 曝露 \_ 相对属性指定电子快门速度。

## <span id="ddk_ksproperty_cameracontrol_exposure_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是指定相机相对曝光设置的 LONG。 步骤大小与硬件相关。 若要确定步长大小，可以在 [**KSPROPERTY \_ CAMERACONTROL \_ 曝露**](ksproperty-cameracontrol-exposure.md) 属性上发出 get 请求。

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
<td><p>将 "公开时间" 设置为特定于实现的默认值。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>按一个步骤递增曝光时间。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>按一个步骤减少曝光时间。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

发出集请求时，应提供 KSPROPERTY CAMERACONTROL 节点的 **值** 成员的上一个表中的值之一 \_ \_ \_ 。

发出 get 请求时，客户端将接收 KSPROPERTY \_ CAMERACONTROL \_ 节点 S 结构的值成员中前一个表中的值之一 \_ 。 值指示照相机的当前曝光时间设置。

如果自动曝光模式控件处于自动模式或口径优先级模式，则设置请求将会失败。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>适用于 windows Vista 和更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

