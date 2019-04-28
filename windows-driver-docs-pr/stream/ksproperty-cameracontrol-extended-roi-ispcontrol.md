---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_ISPCONTROL
description: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_ISPCONTROL KSPROPERTY 中定义的属性 ID\_CAMERACONTROL\_扩展\_属性枚举用于获取或配置的 ROI 设置和应用所需的处理。
ms.assetid: 47F6C327-3279-44C2-9B18-50E6EC9C5E77
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ROI_ISPCONTROL 流式处理媒体设备
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
ms.openlocfilehash: 2fd09ba9f2267d5a5e78493eff0b4ae42aa35715
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351849"
---
# <a name="kspropertycameracontrolextendedroiispcontrol"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_ISPCONTROL

**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_ISPCONTROL**中定义的属性 ID [ **KSPROPERTY\_CAMERACONTROL\_扩展\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)枚举用于获取或配置的 ROI 设置和应用所需的处理。

## <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控件</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Filter</p></td>
<td><p>异步的可取消</p></td>
</tr>
</tbody>
</table>

若要从驱动程序中获取当前的投资回报率设置或若要配置的 ROI 设置和应用所需的处理 (3As) **KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报率\_ISPCONTROL**扩展的属性控制发送到标准以及驱动程序[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构跟[**KSCAMERA\_EXTENDEDPROP\_投资回报率\_ISPCONTROLHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)结构跟[ **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)结构，再按一个或多个相应 ISP 特定控件有效负载的结构。 以下列表说明了一种数据结构布局有一个焦点投资回报率和两个风险投资回报率。

-   **KSCAMERA\_EXTENDEDPROP\_HEADER**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**

-   **KSCAMERA\_EXTENDEDPROP\_投资回报率\_ISPCONTROL** （焦点）

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_FOCUS**

-   **KSCAMERA\_EXTENDEDPROP\_投资回报率\_ISPCONTROL** （使用 2 个 ROIs 公开）

-   **KSCAMERA\_EXTENDEDPROP\_投资回报率\_暴露**(ROI 1)

-   **KSCAMERA\_EXTENDEDPROP\_投资回报率\_暴露**(ROI 2)

下表包含的说明和要求**KSCAMERA\_EXTENDEDPROP\_标头**结构字段时使用**KSPROPERTY\_CAMERACONTROL\_扩展\_ROI\_ISPCONTROL**扩展的投资回报率控件的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>这必须是 1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xFFFFFFFF)</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>对于初始的 GET 调用 （如果没有集调用曾经发生） 这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROLHEADER</strong>)。 此外，驱动程序必须在其 ISO 控制标头有效负载中返回 ControlCount。</p>
<p>为任何其他 SET 或 GET 调用，这必须是 sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ ROI_ISPCONTROLHEADER</strong>) + ControlCount * sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROL</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_ROI_FOCUS</strong>) * ROICount(focus) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_EXPOSURE</strong>) * ROICount (暴露） + sizeof (<strong>KSCAMERA_EXTENDEDPROP_WHITEBALANCE</strong>) * ROICount(whitebalance)。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这表示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。 值 0 指示已检测到任何错误的所有配置的 ISP 控件。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是的按位 OR <strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCONTROL</strong>并<strong>KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE</strong>。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是这可能是一个读/写字段<strong>KSCAMERA_EXTENDEDPROP_FLAG_CANCELOPERATION</strong>集调用。 这必须为 0 的 GET 调用。</p></td>
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
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
