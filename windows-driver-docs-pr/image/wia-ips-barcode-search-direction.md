---
title: WIA\_IPS\_条形码\_搜索\_方向
description: WIA\_IPS\_条形码\_搜索\_方向属性用于配置设备搜索每个扫描的文档页上的条形码 （相对于扫描方向） 的方向。
ms.assetid: 8A328AEE-EAFD-4282-B902-D29BB8175461
keywords:
- WIA_IPS_BARCODE_SEARCH_DIRECTION 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_SEARCH_DIRECTION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b727e046055c0baf2de077f4e916b6824b8823d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370647"
---
# <a name="wiaipsbarcodesearchdirection"></a>WIA\_IPS\_条形码\_搜索\_方向


**WIA\_IPS\_条形码\_搜索\_方向**属性用于配置设备搜索每个上的条形码 （相对于扫描方向） 的方向扫描的文档页。




属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_条形码\_搜索\_方向**属性。

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
<td><p>WIA_BARCODE_HORIZONTAL_SEARCH</p></td>
<td><p>设备水平搜索的条形码。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_VERTICAL_SEARCH</p></td>
<td><p>设备垂直搜索的条形码。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_HORIZONTAL_VERTICAL_SEARCH</p></td>
<td><p>设备搜索条形码首先水平然后垂直。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_VERTICAL_HORIZONTAL_SEARCH</p></td>
<td><p>设备搜索条形码的第一次垂直然后水平。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_AUTO_SEARCH</p></td>
<td><p>设备搜索中，自动在运行时检测到或预定义其自身方向的条形码。</p></td>
</tr>
</tbody>
</table>

 

此属性是必需的所有条码读取器项，但它可以实现以支持仅 WIA\_条形码\_自动\_搜索值。

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

 

 





