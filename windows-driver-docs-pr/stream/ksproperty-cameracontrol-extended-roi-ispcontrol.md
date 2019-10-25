---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_ISPCONTROL
description: KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_在 KSPROPERTY\_CAMERACONTROL 中定义 ISPCONTROL 属性 ID\_扩展\_属性枚举用于获取或配置 ROI 设置和应用所需的处理。
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
ms.openlocfilehash: 2b8e79ec63ea37191d1038c9498e18bf0725a140
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823953"
---
# <a name="ksproperty_cameracontrol_extended_roi_ispcontrol"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_ISPCONTROL

**KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_ISPCONTROL**属性 ID 在[**KSPROPERTY\_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)中定义属性枚举用于获取或配置 ROI 设置并应用所需的处理。

## <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p>异步，可取消</p></td>
</tr>
</tbody>
</table>

若要从驱动程序获取当前的 ROI 设置或配置 ROI 设置并应用所需的处理（3As）， **KSPROPERTY\_CAMERACONTROL\_扩展\_投资回报\_ISPCONTROL**扩展属性控制发送到驱动程序连同标准的[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构，后跟[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)结构后跟[**KSCAMERA\_EXTENDEDPROP\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)结构，然后按一个或多个特定的 ISP 特定控制负载结构\_投资回报率。 下面的列表说明了具有一个焦点 ROI 和两个 ROIs 的数据结构布局。

-   **KSCAMERA\_EXTENDEDPROP\_标头**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL** （焦点）

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_重点**

-   **KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL** （通过 2 ROIs 公开）

-   **KSCAMERA\_EXTENDEDPROP\_roi\_暴露**（roi 1）

-   **KSCAMERA\_EXTENDEDPROP\_roi\_暴露**（roi 2）

下表包含**KSCAMERA\_\_EXTENDEDPROP**的说明和要求，其中使用**KSPROPERTY\_CAMERACONTROL\_扩展\_ROI\_ISPCONTROL**扩展 ROI 控件的属性。

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
<td><p>版本</p></td>
<td><p>这必须为1，</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> （0xffffffff），</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>对于初始 GET 调用（从未发生过任何设置调用），这必须是 sizeof （<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>） + Sizeof （<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROLHEADER</strong>）。 此外，驱动程序在其 ISO 控制标头负载中必须在 ControlCount 中返回0。</p>
<p>对于任何其他设置或获取调用，这必须是 sizeof （<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>） + Sizeof （<strong>KSCAMERA_EXTENDEDPROP_ ROI_ISPCONTROLHEADER</strong>） + ControlCount * sizeof （<strong>KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROL</strong>） + sizeof （<strong>KSCAMERA_EXTENDEDPROP_ROI_FOCUS</strong>） * ROICount （焦点） + sizeof （<strong>KSCAMERA_EXTENDEDPROP_EXPOSURE</strong>） * ROICount （曝光） + sizeof （<strong>KSCAMERA_EXTENDEDPROP_WHITEBALANCE</strong>） * ROICount （WHITEBALANCE）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>这指示上次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。 值0表示未检测到所有配置的 ISP 控件出现错误。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>这必须是<strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCONTROL</strong>和<strong>KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE</strong>。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段，这可能是对集调用<strong>KSCAMERA_EXTENDEDPROP_FLAG_CANCELOPERATION</strong>的。 对于 GET 调用，此必须为0。</p></td>
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
