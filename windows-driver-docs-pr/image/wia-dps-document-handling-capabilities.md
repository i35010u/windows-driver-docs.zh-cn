---
title: WIA\_DPS\_文档\_处理\_功能
description: WIA\_DPS\_文档\_处理\_功能属性包含扫描程序的功能。
ms.assetid: 19c9cbd0-19ef-4d44-85f1-25e71f9a92bc
keywords:
- WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20762860ae8d4239a9ec93b064b596b9ebc6d6a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335460"
---
# <a name="wiadpsdocumenthandlingcapabilities"></a>WIA\_DPS\_文档\_处理\_功能


WIA\_DPS\_文档\_处理\_功能属性包含扫描程序的功能。

## <span id="ddk_wia_dps_document_handling_capabilities_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPS\_文档\_处理\_功能属性来确定扫描程序有平板、 文档送纸器或双面打印器安装。 此属性还可用于进一步定义已安装的功能。 WIA 微型驱动程序创建并维护此属性。

下表介绍才有效，且 Windows 8 的常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>印刷器</p></td>
<td><p>印刷器</p></td>
</tr>
<tr class="even">
<td><p>印记签署器</p></td>
<td><p>印记签署器</p></td>
</tr>
<tr class="odd">
<td><p>BARCODE_READER</p></td>
<td><p>条形码读取器</p></td>
</tr>
<tr class="even">
<td><p>PATCH_CODE_READER</p></td>
<td><p>修补程序代码读取器</p></td>
</tr>
<tr class="odd">
<td><p>MICR_READER</p></td>
<td><p>MICR 读取器</p></td>
</tr>
</tbody>
</table>

 

下表介绍才有效，且 Windows 7 的常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AUTO_SOURCE</p></td>
<td><p>设备支持<a href="https://msdn.microsoft.com/library/windows/hardware/ff539393" data-raw-source="[auto-configured scanning](https://msdn.microsoft.com/library/windows/hardware/ff539393)">自动配置扫描</a>。</p></td>
</tr>
</tbody>
</table>

 

下表描述了与 Windows 7 和 Windows Vista 中，有效的常量，但不能与 Windows XP。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ADVANCED_DUP</p></td>
<td><p>此设备上每个文档大小独立支持高级双工扫描配置。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_FILM_TPA</p></td>
<td><p>准备好扫描透明度或电影扫描适配器时，可以检测到扫描程序。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_STOR</p></td>
<td><p>在内部存储中的文档时，可以检测到扫描程序。</p></td>
</tr>
<tr class="even">
<td><p>FILM_TPA</p></td>
<td><p>扫描程序有一个透明度或电影扫描适配器。</p></td>
</tr>
<tr class="odd">
<td><p>存储帐户</p></td>
<td><p>扫描程序配备有一个内部存储设备。</p></td>
</tr>
</tbody>
</table>

 

下表描述了与 Windows 7、 Windows Vista 和 Windows XP 有效的常量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DETECT_FEED</p></td>
<td><p>扫描程序可以检测文档送纸器中。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_FLAT</p></td>
<td><p>扫描程序可以检测平板辊上的文档。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_SCAN</p></td>
<td><p>扫描程序可以检测文档送纸器中仅通过扫描。</p></td>
</tr>
<tr class="even">
<td><p>DUP</p></td>
<td><p>在扫描仪带有双面打印器。</p></td>
</tr>
<tr class="odd">
<td><p>源</p></td>
<td><p>在扫描仪带有文档送纸器安装。</p></td>
</tr>
<tr class="even">
<td><p>平面</p></td>
<td><p>在扫描仪带有平板辊。</p></td>
</tr>
</tbody>
</table>

 

下表描述了; 仅是与 Windows XP 有效的常量这些标志已过时适用于 Windows 7 和 Windows Vista，并且不应使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DETECT_DUP</p></td>
<td><p>扫描程序可检测到来自用户的双工扫描请求。</p></td>
</tr>
<tr class="even">
<td><p>DETECT_DUP_AVAIL</p></td>
<td><p>双面打印器安装时，可以检测到扫描程序。</p></td>
</tr>
<tr class="odd">
<td><p>DETECT_FEED_AVAIL</p></td>
<td><p>安装文档送纸器时，可以检测到扫描程序。</p></td>
</tr>
</tbody>
</table>

 

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

 

 





