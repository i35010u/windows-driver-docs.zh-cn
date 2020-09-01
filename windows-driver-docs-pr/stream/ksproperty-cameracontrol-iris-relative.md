---
title: KSPROPERTY \_ CAMERACONTROL \_ IRIS \_ 相对
description: KSPROPERTY \_ CAMERACONTROL \_ IRIS \_ 相对属性指定相机的口径设置。
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
ms.openlocfilehash: b9a15ae1ffe68550f7e9aa26564ca0b6f22e1f8e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192535"
---
# <a name="ksproperty_cameracontrol_iris_relative"></a>KSPROPERTY \_ CAMERACONTROL \_ IRIS \_ 相对


KSPROPERTY \_ CAMERACONTROL \_ IRIS \_ 相对属性指定相机的口径设置。

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
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是指定相机的相对 iris 设置的 LONG。 请注意，iris 步长大小和 iris 步骤默认值都是特定于实现的。

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

 

<a name="remarks"></a>注解
-------

发出集请求时，应提供 KSPROPERTY CAMERACONTROL 节点的 **值** 成员的上一个表中的值之一 \_ \_ \_ 。

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
<td><p>Header</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

