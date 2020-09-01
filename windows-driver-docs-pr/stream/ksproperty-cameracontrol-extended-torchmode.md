---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ TORCHMODE
description: Torch 模式决定了照相机的闪光在轻型条件下的使用方式。
ms.assetid: FB168F4E-EBF9-4925-B4F1-BC9305DB0109
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ecf7fb3baa09bded8fe1efb04d13c8addd3e03ee
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186586"
---
# <a name="ksproperty_cameracontrol_extended_torchmode"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ TORCHMODE

Torch 模式决定了照相机的闪光在轻型条件下的使用方式。 闪光会持续提供较低的强度光源，以便为自动聚焦等操作提供足够的光源。

## <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) 结构。

总的属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ VALUE) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含驱动程序支持的以下一种或多种 TORCH 模式的按位 "或" 组合。

| Torch 模式                                              | 说明                                      |
|---------------------------------------------------------|--------------------------------------------------|
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOTORCH \_ OFF                 | Torchlight 为 off。                               |
| KSCAMERA \_ EXTENDEDPROP \_ VIDEOTORCH \_                  | Torchlight 处于默认强度级别。 |
| \_ \_ \_ ADJUSTABLEPOWER 上的 KSCAMERA EXTENDEDPROP VIDEOTORCH \_ | Torchlight 在特定的电源级别打开。      |

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的 torch 模式。 照相机的默认 torch 模式为 KSCAMERA \_ EXTENDEDPROP \_ VIDEOTORCH \_ OFF，驱动程序必须支持此 torch 模式。

此属性控件是同步的，不可取消。

## <a name="remarks"></a>备注

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
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) </p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>支持 Torch 模式值。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前 torch 模式值设置 (仅) 一个值。</td>
</tr>
</tbody>
</table>

如果 torch 模式为 \_ ADJUSTABLEPOWER 上的 KSCAMERA EXTENDEDPROP \_ VIDEOTORCH \_ \_ ，则[**u) \_ KSCAMERA \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)的**EXTENDEDPROP**成员的值将包含介于 0-100 之间的强度级别值。 强度值为0，表示最小级别为100，表示最大强度级别。

如果之前未设置任何场景模式，则将 **标志** 设置为 KSCAMERA \_ EXTENDEDPROP \_ VIDEOTORCH \_ OFF (默认) 。

### <a name="setting-the-property"></a>设置属性

如果设置了属性，则 KSPROPERTY \_ 类型 \_ 集请求， [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的 torch 模式。 如果**Flags**为 KSCAMERA **Value.ull** EXTENDEDPROP VIDEOTORCH [** \_ \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) \_ \_ \_ ON \_ ADJUSTABLEPOWER，则 KSCAMERA EXTENDEDPROP 值的 u) 成员将包含设置的强度级别。

## <a name="requirements"></a>要求

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

[**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)