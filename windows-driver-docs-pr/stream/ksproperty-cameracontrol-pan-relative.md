---
title: KSPROPERTY\_CAMERACONTROL\_平移\_相对
description: KSPROPERTY\_CAMERACONTROL\_平移\_相对属性指定照相机的绕垂直轴的旋转角度。
ms.assetid: 11b6ac3e-e65e-4a85-bfcc-f45e8e96c8fb
keywords:
- KSPROPERTY_CAMERACONTROL_PAN_RELATIVE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PAN_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a114d62d61926242fca5152e9ae705f629c14b1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575769"
---
# <a name="kspropertycameracontrolpanrelative"></a>KSPROPERTY\_CAMERACONTROL\_平移\_相对


KSPROPERTY\_CAMERACONTROL\_平移\_相对属性指定照相机的绕垂直轴的旋转角度。

## <span id="ddk_ksproperty_cameracontrol_pan_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PAN_RELATIVE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的相对平移设置长时间。 值的大小表示所需的平移速度;较高的值表示较高的速度。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>停止平移。</p></td>
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

 

<a name="remarks"></a>备注
-------

**值**的成员[ **KSPROPERTY\_CAMERACONTROL\_节点\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff564420)结构指定相对平移。

请注意，特定设备可能仅支持某些速度范围。 若要确定设备支持的速度的范围，应用程序可以发出 KSPROPERTY\_类型\_BASICSUPPORT 请求。 您可以指定 KSPROPERTY\_类型\_中的 BASICSUPPORT**标志**的成员[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)结构。

有些设备支持仅以单个平移的速度。 在本示例中的符号**值**成员指示方向平移。

在 set 请求时，客户端应提供在上表中的值之一**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。

在 get 请求时，客户端收到的值之一前面表中**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。 值指示的照相机的当前平移状态。

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
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY\_CAMERACONTROL\_节点\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564420)

 

 






