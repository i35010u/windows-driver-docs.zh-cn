---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ EVCOMPENSATION
description: EV 补偿属性允许按曝光度或区域系统的增量调整公开控制。
ms.assetid: 1109C533-89CA-4A23-BCF9-D44C28C0C6BF
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5e21c8853b63af0b23995dc895a50f3c9188cbdb
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104838"
---
# <a name="ksproperty_cameracontrol_extended_evcompensation"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ EVCOMPENSATION


EV 补偿属性允许按曝光度或区域系统的增量调整公开控制。

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
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ EVCOMPENSATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation) 结构。

总属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ EVCOMPENSATION) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个补偿设置的按位 "或" 组合。

| EV 补偿单步执行                    | 说明                                                             |
|---------------------------------------------|-------------------------------------------------------------------------|
| KSCAMERA \_ EXTENDEDPROP \_ EVCOMP \_ SIXTHSTEP   | 在公开值的第六个 (1/6) 步骤中，EV 补偿更改。  |
| KSCAMERA \_ EXTENDEDPROP \_ EVCOMP \_ QUARTERSTEP | EV 值的一个四 (1/4) 步骤中的 EV 补偿更改。 |
| KSCAMERA \_ EXTENDEDPROP \_ EVCOMP \_ THIRDSTEP   | EV 值的第三 (1/3) 步骤中的 EV 更改。  |
| KSCAMERA \_ EXTENDEDPROP \_ EVCOMP \_ HALFSTEP    | 在公开值的 (1/2) 步骤中，EV 补偿更改。   |
| KSCAMERA \_ EXTENDEDPROP \_ EVCOMP \_ FULLSTEP    | EV 值 (1/1) 步骤中的 EV 更改。        |

 

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含照相机的当前 EV 补偿步进 (一个) 值。建议使用驱动程序公布仅针对最小 EV 补偿步骤大小的支持。

此属性控件是异步的，不可取消。

<a name="remarks"></a>注解
-------

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 的成员设置为以下项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td> (0xFFFFFFFF) KSCAMERA_EXTENDEDPROP_FILTERSCOPE。</td>
</tr>
<tr class="odd">
<td>大小</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_EVCOMPENSATION) </p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>驱动程序支持的单步执行标志。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前步进值集。</td>
</tr>
</tbody>
</table>

 

驱动程序将当前 EV 补偿单步执行 **标记**。 [**KSCAMERA \_ EXTENDEDPROP \_ EVCOMPENSATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)的成员指示当前步骤单元范围以及用于补偿的步骤数

### <a name="setting-the-property"></a>设置属性

如果设置了该属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**FLAGS**成员将包含要使用的 EV 补偿单步。 用于补偿的新步骤单位数是在[**KSCAMERA \_ EXTENDEDPROP \_ EVCOMPENSATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)的**Value**成员中设置的。

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
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ EVCOMPENSATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)