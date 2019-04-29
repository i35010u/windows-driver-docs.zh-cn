---
title: WIA\_IPS\_CUR\_意向
description: WIA\_IPS\_CUR\_意向属性包含的图像的应用程序的预期用途的当前设置。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 9fa732bb-9281-441e-91b5-ce6eec67ea8f
keywords:
- WIA_IPS_CUR_INTENT 成像设备
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
ms.openlocfilehash: b8aa665d3abfe02727ae70bea93f62c1f6b22405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370613"
---
# <a name="wiaipscurintent"></a>WIA\_IPS\_CUR\_意向


WIA\_IPS\_CUR\_意向属性包含的图像的应用程序的预期用途的当前设置。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ips_cur_intent_si"></span><span id="DDK_WIA_IPS_CUR_INTENT_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_FLAG

访问权限：读取/写入

<a name="remarks"></a>备注
-------

驱动程序使用的意向的设置来预设置基于应用程序的预期用途的图像的项属性。 例如，这些属性可能包括最大的质量和最小大小。

下表包含图像类型标志和它们的定义。 这些标志用于设置面向哪种类型的映像： 颜色、 灰度，等等。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>映像类型标志</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_INTENT_IMAGE_TYPE_COLOR</p></td>
<td><p>该应用程序计划准备为颜色扫描设备。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_IMAGE_TYPE_GRAYSCALE</p></td>
<td><p>该应用程序计划准备为灰度扫描设备。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_IMAGE_TYPE_TEXT</p></td>
<td><p>该应用程序计划准备设备进行扫描的文本。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_IMAGE_TYPE_MASK</p></td>
<td><p>此标志是所有的图像类型标志的掩码。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_NONE</p></td>
<td><p>默认值。 指定没有意向。</p></td>
</tr>
</tbody>
</table>

 

下表包含图像大小和质量标志和它们的定义。 这些标志用于设置的大小和映像扫描的质量。

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
<td><p>该应用程序准备设备进行扫描预览计划。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_MAXIMIZE_QUALITY</p></td>
<td><p>该应用程序计划准备适用于扫描的高质量映像的设备。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_INTENT_MINIMIZE_SIZE</p></td>
<td><p>该应用程序准备好进行扫描的图像的小型扫描会导致设备计划。</p></td>
</tr>
<tr class="even">
<td><p>WIA_INTENT_SIZE_MASK</p></td>
<td><p>此标志是所有的大小和质量的标志掩码。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序选择位深度，以每英寸和其他设置，它确定适用于所选的意图。 应用程序必须读取的当前设置，以确定哪些属性已更改。

应用程序设置 WIA\_IPS\_CUR\_意向属性来自动设置特定获取意向的 WIA 属性。 请注意，可以使用按位 OR 运算符，组合标志，但图像不能为灰度和颜色。

WIA\_IPS\_CUR\_意图是所必需的所有图像采集启用项; 它不是可用于存储项目或存储的图像项。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





