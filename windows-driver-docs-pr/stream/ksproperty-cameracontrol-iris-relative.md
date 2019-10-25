---
title: KSPROPERTY\_CAMERACONTROL\_IRIS\_相对
description: KSPROPERTY\_CAMERACONTROL\_IRIS\_相对属性指定相机的口径设置。
ms.assetid: 919fcf7a-ee96-4e1e-b0ce-e5a7ce5086c7
keywords:
- KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4952ae28463244efa358d843fd2ddf1d660b59cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843352"
---
# <a name="ksproperty_cameracontrol_iris_relative"></a>KSPROPERTY\_CAMERACONTROL\_IRIS\_相对


KSPROPERTY\_CAMERACONTROL\_IRIS\_相对属性指定相机的口径设置。

## <span id="ddk_ksproperty_cameracontrol_iris_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE_KS"></span>


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
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定相机的相对 iris 设置的 LONG。 请注意，iris 步长大小和 iris 步骤默认值都是特定于实现的。

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
<td><p>将 iris 设置为默认打开。 此默认值是特定于实现并在硬件中提供的。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>打开 iris 一步。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>关闭 iris。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

发出集请求时，应提供 KSPROPERTY\_CAMERACONTROL\_\_NODE 的**值**成员的上表中的值之一。

如果自动曝光模式控件处于自动模式或快门优先级模式，则设置请求将会失败。

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

 

 






