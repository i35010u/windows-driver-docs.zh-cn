---
title: WIA\_IP\_分段
description: WIA\_IP\_分段属性指示是否要在扫描期间执行分段。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 4e801aa4-a85f-4439-8a8d-990e6cbf81e4
keywords:
- WIA_IPS_SEGMENTATION 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SEGMENTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6ed0ba88a16d034ad9c9398899f766e8aa9da9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541216"
---
# <a name="wiaipssegmentation"></a>WIA\_IP\_分段


WIA\_IP\_分段属性指示是否要在扫描期间执行分段。 WIA 微型驱动程序创建并维护此属性。

属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

下表描述了为 WIA 定义的值\_IP\_分段属性。

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
<td><p>WIA_USE_SEGMENTATION_FILTER</p></td>
<td><p>应用程序应使用多区域扫描分段筛选器。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DONT_USE_SEGMENTATION_FILTER</p></td>
<td><p>该驱动程序创建子项目本身进行多区域扫描。 如果扫描程序的多区域扫描使用固定的帧，通常会发生这种情况。</p></td>
</tr>
</tbody>
</table>

 

必须实现 WIA\_IP\_扫描程序平板和电影胶片的分段项如果它们使用分段筛选器支持子项目的创建或驱动程序本身创建子固定帧的项。

可以使用分段筛选器驱动程序文件打包，并且对 WIA\_IPS\_设置为 WIA 的分段\_不\_使用\_分段\_筛选器的一个项 (例如，电影项）。 如果有关电影扫描，而不是扫描从平板扫描仪使用固定的帧，则可能出现此情况。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





