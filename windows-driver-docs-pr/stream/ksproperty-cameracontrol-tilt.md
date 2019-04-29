---
title: KSPROPERTY\_CAMERACONTROL\_倾斜
description: 用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_倾斜属性来获取或设置照相机的倾斜度设置。 此属性为可选项。
ms.assetid: 265315ce-6f35-4f5a-907f-b5595e7fb5af
keywords:
- KSPROPERTY_CAMERACONTROL_TILT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_TILT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a0fe3f77cc5e1e36424b38e5d1f64d198b71fdb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381109"
---
# <a name="kspropertycameracontroltilt"></a>KSPROPERTY\_CAMERACONTROL\_倾斜


用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_倾斜属性来获取或设置照相机的倾斜度设置。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_tilt_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_TILT_KS"></span>


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

 

属性值 （操作数据） 为指定照相机的倾斜度设置长时间。 此值表示以度为单位。

正值点成像平面上。 负值成像平面指向下方，如下图中所示。

![图显示相机倾斜值](images/cam-tilt-1.png)

每个视频捕获微型驱动程序支持此属性必须定义此属性的范围和默认值。 设备的范围必须介于-180 到 180。 默认值必须为 0。

**谨慎**  在编写或测试的应用程序，您应注意到，在实践中，某些驱动程序定义的倾斜值和自定义步骤值可能不基于典型单位的自定义范围。 驱动程序可能会实现倾斜控件以物理方式或数字。

 

<a name="remarks"></a>备注
-------

**值**KSPROPERTY 成员\_CAMERACONTROL\_S 结构指定倾斜设置。

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

 

 






