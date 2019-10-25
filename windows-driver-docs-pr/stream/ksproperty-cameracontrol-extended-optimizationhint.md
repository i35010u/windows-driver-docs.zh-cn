---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_OPTIMIZATIONHINT
description: 照相机驱动程序可以根据应用程序提供的提示来优化其捕获操作。 此属性通知驱动程序根据可能使用最多的操作来设置其性能策略。
ms.assetid: FEA3D355-B490-4E67-905D-EE5507E91150
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: afee622ffb06489a7cbc2c3580f557b91be5355a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841589"
---
# <a name="ksproperty_cameracontrol_extended_optimizationhint"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_OPTIMIZATIONHINT

照相机驱动程序可以根据应用程序提供的提示来优化其捕获操作。 此属性通知驱动程序根据可能使用最多的操作来设置其性能策略。 例如，当针对照片进行了优化时，照相机驱动程序可以对传感器进行编程以优化传感器的曝光速度和分辨率，以降低从照片捕获触发器到映像捕获的延迟。 同样，在对视频进行优化时，照相机驱动程序可以对传感器编程更高的帧速率，但会降低分辨率。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>“是”</p></td>
<td><p>Filter</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值（操作数据）包含[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构和[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)结构。

总属性数据大小为**sizeof**（KSCAMERA\_EXTENDEDPROP\_标头） + **sizeof**（KSCAMERA\_EXTENDEDPROP\_值）。 [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Size**成员设置为此总属性数据大小。

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**功能**成员包含以下一个或多个优化提示的按位 "或" 组合。

| 优化提示                           | 描述                               |
|---------------------------------------------|-------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_优化\_照片 | 照相机操作针对照片进行了优化。 |
| KSCAMERA\_EXTENDEDPROP\_优化\_视频 | 相机操作经过优化，可用于视频。  |

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员包含当前为相机设置的优化（一个值）。

默认优化类型为 KSCAMERA\_EXTENDEDPROP\_优化\_照片。 如果相机驱动程序支持此属性，则必须同时支持这两种优化类型。

此属性控件是同步的，不可取消。

## <a name="remarks"></a>备注

### <a name="optimization-modes"></a>优化模式

**KSCAMERA\_EXTENDEDPROP\_优化\_照片**
-   所有照相机驱动程序都必须处于此模式下，直到明确知道使用 KSCAMERA\_EXTENDEDPROP\_优化\_视频模式。 此模式的目的是针对照片操作优化相机硬件。 视频操作在此模式下仍必须正常运行。

**KSCAMERA\_EXTENDEDPROP\_优化\_视频**
-   此模式表示相机可能会用于视频操作。 照相机驱动程序应该优化此模式的视频操作硬件。 照片操作必须正常运行，但对于视频操作，资源使用优先级。

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY\_类型\_GET 请求时，驱动程序会将[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的成员设置为以下项。

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
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_VALUE）</p></td>
</tr>
<tr class="even">
<td>结果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>功能</td>
<td>支持的优化值。</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>当前优化值设置。</td>
</tr>
</tbody>
</table>

如果以前未设置优化模式，则驱动程序会将**标志**设置为 KSCAMERA\_EXTENDEDPROP\_优化\_照片（默认值）。

### <a name="setting-the-property"></a>设置属性

设置属性时，KSPROPERTY\_类型\_SET 请求， [**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的**Flags**成员将包含要设置的 optomization 模式。

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
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
