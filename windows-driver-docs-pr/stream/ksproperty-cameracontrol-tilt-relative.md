---
title: KSPROPERTY\_CAMERACONTROL\_倾斜度\_相对
description: KSPROPERTY\_CAMERACONTROL\_斜度\_相对属性指定相机的垂直倾斜状态。
ms.assetid: 82702eec-38dc-44a1-bf57-56c9f04bb2d0
keywords:
- KSPROPERTY_CAMERACONTROL_TILT_RELATIVE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_TILT_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd8909c8ddb385755857b534f499361326bd9113
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842481"
---
# <a name="ksproperty_cameracontrol_tilt_relative"></a>KSPROPERTY\_CAMERACONTROL\_倾斜度\_相对


KSPROPERTY\_CAMERACONTROL\_斜度\_相对属性指定相机的垂直倾斜状态。

## <span id="ddk_ksproperty_cameracontrol_tilt_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_TILT_RELATIVE_KS"></span>


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

 

属性值（操作数据）是指定相机相对倾斜设置的 LONG。 值的大小表示所需的倾斜速度;较高的值表示较高的速度。

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
<td><p>停止倾斜。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>启动倾斜。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始倾斜。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[**KSPROPERTY\_CAMERACONTROL\_NODE\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)结构的**值**成员指定了相对倾斜。

请注意，特定设备可能仅支持特定的速度范围。 若要确定设备支持的速度范围，应用程序可以\_BASICSUPPORT 请求发出 KSPROPERTY\_类型。 可以在[**KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)结构的**Flags**成员中指定 KSPROPERTY\_类型\_BASICSUPPORT。

某些设备仅支持一个倾斜速度。 在这种情况下，**值**成员的符号指示要倾斜的方向。

发出集请求时，客户端应提供 KSPROPERTY\_CAMERACONTROL\_NODE\_结构的**值**成员的上一个表中的值之一。

发出 get 请求时，客户端将接收 KSPROPERTY\_CAMERACONTROL\_NODE\_结构的**值**成员的上表中的值之一。 值指示照相机的当前倾斜状态。

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

 

 






