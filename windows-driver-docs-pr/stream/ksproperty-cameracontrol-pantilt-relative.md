---
title: KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对
description: KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对属性指定的照相机水平或垂直旋转，并可以同时指定两者。
ms.assetid: c2c9405c-7713-439f-a150-51969a2a5e6b
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc01cdc7ec9bb6acc00ca933db27e59d1819ba50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526835"
---
# <a name="kspropertycameracontrolpantiltrelative"></a>KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对


KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对属性指定的照相机水平或垂直旋转，并可以同时指定两者。

## <span id="ddk_ksproperty_cameracontrol_pantilt_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564421" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564421)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff564451" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564451)"> <strong>KSPROPERTY_CAMERACONTROL_S2</strong> </a>具体取决于该请求是一个筛选器或节点</p></td>
<td><p>对长整数</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一对指定照相机的相对平移和倾斜设置的长整数。 值的大小表示所需的平移速度;较高的值表示较高的速度。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值 1</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>停止照相机水平的运动。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>开始向右平移。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始向左平移。</p></td>
</tr>
</tbody>
</table>

 

值的大小表示所需的倾斜速度;较高的值表示较高的速度。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value2</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>停止的照相机垂直的动作。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>开始向上旋转照相机。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始向下旋转照相机。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要进行平移照相机的集请求时，客户端应提供在上表中的值之一**Value1**属性描述符结构的成员。

同样，set 请求来倾斜照相机时，客户端提供在上表中的值之一**Value2**属性描述符结构的成员。

客户端时发出 get 请求，接收中的平移值**Value1**中的成员以及倾斜值**Value2** KSPROPERTY 成员\_CAMERACONTROL\_S2 或KSPROPERTY\_CAMERACONTROL\_节点\_S2 结构。 值指示当前平移或倾斜的相机的状态。

请注意，特定设备可能仅支持某些速度范围。 若要确定设备支持的速度的范围，应用程序可以发出 KSPROPERTY\_类型\_BASICSUPPORT 请求。 您可以指定 KSPROPERTY\_类型\_中的 BASICSUPPORT**标志**的成员[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)结构。

某些设备支持单个平移或倾斜速度。 在本示例中的符号**Value1**或**Value2**成员指示方向平移。

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
<td><p>适用于 Windows Vista 和更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY\_CAMERACONTROL\_S2**](https://msdn.microsoft.com/library/windows/hardware/ff564451)

[**KSPROPERTY\_CAMERACONTROL\_节点\_S2**](https://msdn.microsoft.com/library/windows/hardware/ff564421)

 

 






