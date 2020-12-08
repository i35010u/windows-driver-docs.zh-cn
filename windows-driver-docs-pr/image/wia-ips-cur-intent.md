---
title: WIA \_ IP \_ 当前 \_ 意向
description: WIA ip 的 "当前 \_ \_ 意向" \_ 属性包含应用程序预期的映像用途的当前设置。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_CUR_INTENT 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_CUR_INTENT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4e0021989e661c8d99ec706d61e3ed6aa5d350c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796145"
---
# <a name="wia_ips_cur_intent"></a>WIA \_ IP \_ 当前 \_ 意向


WIA ip 的 "当前 \_ \_ 意向" \_ 属性包含应用程序预期的映像用途的当前设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_cur_intent_si"></span><span id="DDK_WIA_IPS_CUR_INTENT_SI"></span>


属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 标志

访问权限：读/写

<a name="remarks"></a>备注
-------

驱动程序使用意向设置根据应用程序的映像用途预设置项属性。 这些属性可能包括最高质量和最小大小。

下表包含图像类型标志及其定义。 这些标志用于设置预期类型的图像：颜色、灰度等。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>图像类型标志</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_INTENT_IMAGE_TYPE_COLOR</p></td>
<td><p>应用程序打算为彩色扫描准备设备。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_IMAGE_TYPE_GRAYSCALE</p></td>
<td><p>应用程序打算准备设备以进行灰度扫描。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_IMAGE_TYPE_TEXT</p></td>
<td><p>应用程序打算准备设备以便扫描文本。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_IMAGE_TYPE_MASK</p></td>
<td><p>此标志是所有图像类型标志的掩码。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_NONE</p></td>
<td><p>默认值。 未指定意向。</p></td>
</tr>
</tbody>
</table>

 

下表包含图像大小和质量标志及其定义。 这些标志用于设置图像扫描的大小和质量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>图像大小/质量标志</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_INTENT_BEST_PREVIEW</p></td>
<td><p>应用程序打算准备设备以扫描预览。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_MAXIMIZE_QUALITY</p></td>
<td><p>应用程序打算准备设备，以便扫描高质量的映像。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_MINIMIZE_SIZE</p></td>
<td><p>应用程序打算准备设备，以扫描导致小型扫描的映像。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_SIZE_MASK</p></td>
<td><p>此标志是所有大小和质量标志的掩码。</p></td>
</tr>
</tbody>
</table>

 

驱动程序将选择位深度（以每英寸点数为单位）和它确定的其他设置适用于所选意向。 应用程序必须读取当前设置以确定更改了哪些属性。

应用程序将 "WIA ip" 的 " \_ \_ 目标" 属性设置 \_ 为 "自动设置 wia 属性以获得特定获取意向"。 请注意，标志可以与按位 OR 运算符组合，但图像不能同时为灰度和颜色。

\_ \_ \_ 所有启用了映像采集的项目都需要 WIA ip （当前意向）; 它不适用于存储项或存储的图像项。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





