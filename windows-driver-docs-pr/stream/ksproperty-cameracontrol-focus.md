---
title: KSPROPERTY\_CAMERACONTROL\_焦点
description: 用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_焦点属性来获取或设置照相机的焦点设置。 此属性为可选项。
ms.assetid: 89a77055-1ad1-4394-8435-d057685b9eee
keywords:
- KSPROPERTY_CAMERACONTROL_FOCUS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a65920f9afd7511178d3247f2f595280bac213d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341824"
---
# <a name="kspropertycameracontrolfocus"></a>KSPROPERTY\_CAMERACONTROL\_焦点


用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_焦点属性来获取或设置照相机的焦点设置。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_focus_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCUS_KS"></span>


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

 

属性值 （操作数据） 为指定的焦点设置长时间。 此值是以毫米为单位表示。

**谨慎**  在编写或测试的应用程序，您应注意到在实践中，某些驱动程序定义自定义范围的焦点值和自定义步骤值的不可能基于典型的单位。 驱动程序可能会实现焦点控件以物理方式或数字。

 

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_CAMERACONTROL\_S 结构指定的焦点设置。

每个视频捕获微型驱动程序支持此属性必须定义此属性为其自身范围和默认值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564439)

 

 






