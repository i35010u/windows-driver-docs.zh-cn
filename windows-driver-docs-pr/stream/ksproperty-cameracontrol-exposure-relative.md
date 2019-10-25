---
title: KSPROPERTY\_CAMERACONTROL\_泄露\_相对
description: KSPROPERTY\_CAMERACONTROL\_曝露\_相对属性指定电子快门速度。
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
ms.openlocfilehash: 3039b8c504099530266d6877287fd9c99d5ef3bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843250"
---
# <a name="ksproperty_cameracontrol_exposure_relative"></a>KSPROPERTY\_CAMERACONTROL\_泄露\_相对


KSPROPERTY\_CAMERACONTROL\_曝露\_相对属性指定电子快门速度。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定相机相对曝光设置的 LONG。 步骤大小与硬件相关。 若要确定步长大小，可以在[**KSPROPERTY\_CAMERACONTROL\_曝露**](ksproperty-cameracontrol-exposure.md)属性上发出 get 请求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>描述</th>
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

发出集请求时，应提供 KSPROPERTY\_CAMERACONTROL\_\_NODE 的**值**成员的上表中的值之一。

发出 get 请求时，客户端将接收 KSPROPERTY\_CAMERACONTROL\_NODE\_结构的值成员的上表中的值之一。 值指示照相机的当前曝光时间设置。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_CAMERACONTROL\_NODE\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 






