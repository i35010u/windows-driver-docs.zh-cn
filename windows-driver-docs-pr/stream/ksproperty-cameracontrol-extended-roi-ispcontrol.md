---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 投资回报 \_ ISPCONTROL
description: '\_ \_ \_ \_ KSPROPERTY CAMERACONTROL 扩展属性枚举中定义的 KSPROPERTY CAMERACONTROL 扩展 ROI ISPCONTROL 属性 \_ ID \_ \_ 用于获取或配置 ROI 设置并应用所需的处理。'
ms.assetid: 47F6C327-3279-44C2-9B18-50E6EC9C5E77
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_ISPCONTROL 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_ISPCONTROL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff6ef3be7365c9d126aa09da2f8d7257d2f019ef
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190517"
---
# <a name="ksproperty_cameracontrol_extended_roi_ispcontrol"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 投资回报 \_ ISPCONTROL

[**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 属性**](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举中定义的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ ROI \_ ISPCONTROL**属性 ID 用于获取或配置 ROI 设置并应用所需的处理。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>作用域</th>
<th>控制</th>
<th>类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>筛选器</p></td>
<td><p>异步，可取消</p></td>
</tr>
</tbody>
</table>

若要从驱动程序获取当前的 ROI 设置，或配置 ROI 设置并将所需的处理应用 (3As) ，请将**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ ROI \_ ISPCONTROL**扩展属性控件连同标准[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构一起发送到驱动程序，后面跟有一个 KSCAMERA EXTENDEDPROP roi ISPCONTROLHEADER 结构，然后使用一个或多个特定的 ISP 特定控制负载结构。 [** \_ \_ \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader) [** \_ \_ \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol) 下面的列表说明了具有一个焦点 ROI 和两个 ROIs 的数据结构布局。

-   **KSCAMERA \_ EXTENDEDPROP \_ 标头**

-   **KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ ISPCONTROLHEADER**

-   **KSCAMERA \_EXTENDEDPROP \_ ROI \_ ISPCONTROL** (重点) 

-   **KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ 要点**

-   **KSCAMERA \_利用2个 ROIs) ，EXTENDEDPROP \_ ROI \_ ISPCONTROL** (公开

-   **KSCAMERA \_EXTENDEDPROP \_ \_ ** roi (投资回报率 1) 

-   **KSCAMERA \_EXTENDEDPROP \_ 投资 \_ 回报** 率 (roi 2) 

下表包含了在使用扩展 ROI 控制的**KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ roi \_ ISPCONTROL**属性时， **KSCAMERA \_ EXTENDEDPROP \_ 标头**结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须 <strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xffffffff) ，</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>对于最初的 GET 调用 () 此操作必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + <strong>sizeof (KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROLHEADER) 。</strong> 此外，驱动程序在其 ISO 控制标头负载中必须在 ControlCount 中返回0。</p>
<p>对于任何其他设置或获取调用，这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_</strong> ROI_ISPCONTROLHEADER) + ControlCount * <strong>sizeof (KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROL) +</strong> sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_FOCUS</strong>) * ROICount () + sizeof (<strong>KSCAMERA_EXTENDEDPROP_EXPOSURE</strong>) * ROICount (公开) + <strong>sizeof (KSCAMERA_EXTENDEDPROP_WHITEBALANCE) *</strong> ROICount (WHITEBALANCE) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这指示上次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。 值0表示未检测到所有配置的 ISP 控件出现错误。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是 <strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCONTROL</strong> 和 <strong>KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE</strong>。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段，这可能是对集调用 <strong>KSCAMERA_EXTENDEDPROP_FLAG_CANCELOPERATION</strong> 的。 对于 GET 调用，此必须为0。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>