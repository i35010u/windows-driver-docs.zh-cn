---
title: KSPROPERTY\_CAMERACONTROL\_倾斜\_相对
description: KSPROPERTY\_CAMERACONTROL\_倾斜\_相对属性指定照相机的垂直 tilting 状态。
ms.assetid: 82702eec-38dc-44a1-bf57-56c9f04bb2d0
keywords:
- KSPROPERTY_CAMERACONTROL_TILT_RELATIVE 流式处理媒体设备
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
ms.openlocfilehash: 18ba999460a15325da7c3fa648006ce4108295db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378193"
---
# <a name="kspropertycameracontroltiltrelative"></a>KSPROPERTY\_CAMERACONTROL\_倾斜\_相对


KSPROPERTY\_CAMERACONTROL\_倾斜\_相对属性指定照相机的垂直 tilting 状态。

## <span id="ddk_ksproperty_cameracontrol_tilt_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_TILT_RELATIVE_KS"></span>


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

 

属性值 （操作数据） 为指定照相机的相对倾斜设置长时间。 值的大小表示所需的倾斜速度;较高的值表示较高的速度。

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
<td><p>停止倾斜。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>启动倾斜。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始向下倾斜。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**值**的成员[ **KSPROPERTY\_CAMERACONTROL\_节点\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff564420)结构指定相对倾斜。

请注意，特定设备可能仅支持某些速度范围。 若要确定设备支持的速度的范围，应用程序可以发出 KSPROPERTY\_类型\_BASICSUPPORT 请求。 您可以指定 KSPROPERTY\_类型\_中的 BASICSUPPORT**标志**的成员[ **KSPROPERTY\_项**](https://msdn.microsoft.com/library/windows/hardware/ff565176)结构。

有些设备支持仅将单个倾斜速度。 在本示例中的符号**值**成员指示方向倾斜。

在 set 请求时，客户端应提供在上表中的值之一**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。

在 get 请求时，客户端收到的值之一前面表中**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。 值指示的照相机的当前倾斜状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
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

 

 






