---
title: KSPROPERTY\_CAMERACONTROL\_焦点\_相对
description: KSPROPERTY\_CAMERACONTROL\_焦点\_相对属性指定照相机的焦点设置。
ms.assetid: 8282c703-5ff7-437e-87f9-e05f504d6f2c
keywords:
- KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d44780873485b59c1c683609b54b356d0406fedf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354442"
---
# <a name="kspropertycameracontrolfocusrelative"></a>KSPROPERTY\_CAMERACONTROL\_焦点\_相对


KSPROPERTY\_CAMERACONTROL\_焦点\_相对属性指定照相机的焦点设置。

## <span id="ddk_ksproperty_cameracontrol_focus_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的相对焦点设置长时间。 值的大小表示焦点更改; 的速度较高的值表示较高的速度。

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
<td><p>停止焦点运动。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>开始将更接近的焦点移动到该对象。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始移动将重点更远从该对象。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在 set 请求时，提供在上表中的值之一**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。

在 get 请求时，客户端收到的值之一前面表中**值**KSPROPERTY 成员\_CAMERACONTROL\_节点\_S 结构。 值指示用于相机的当前焦点设置。

请注意，特定设备可能仅支持某些速度范围。 若要确定设备支持的速度的范围，应用程序可以发出 KSPROPERTY\_类型\_BASICSUPPORT 请求。 您可以指定 KSPROPERTY\_类型\_中的 BASICSUPPORT**标志**的成员[ **KSPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_item)结构。

有些设备支持仅以单个焦点的速度。 在本示例中的符号**值**成员只需指示是否可重用功能区应缩短其焦点或延长它。

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


[**KSPROPERTY\_CAMERACONTROL\_节点\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 






