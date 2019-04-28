---
title: WIA\_IPS\_SCAN\_AHEAD
description: WIA\_IPS\_扫描\_预先属性用于启用扫描提前在硬件设备 （扫描在最高可能速度，在扫描程序的内部内存中，将并行缓冲的图像传送缓冲扫描的图像相同或较低的速度的客户端应用）。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 706BA423-399F-4859-BF41-10D3A88B61DD
keywords:
- WIA_IPS_SCAN_AHEAD 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SCAN_AHEAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: deb7b4eff92044ec81894c26214dd44d193ee8ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343861"
---
# <a name="wiaipsscanahead"></a>WIA\_IPS\_SCAN\_AHEAD


**WIA\_IPS\_扫描\_预先**属性用于启用扫描提前在硬件设备 （扫描在最高可能速度，在扫描程序的内部内存中缓冲的扫描的图像传输缓冲映像以并行方式对相同或较低的速度的客户端应用程序）。 WIA 微型驱动程序创建并维护此属性。




**请注意**  此属性替换[ **WIA\_DPS\_扫描\_预先\_页面**](wia-dps-scan-ahead-pages.md)，现已过时。

 

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了的有效值**WIA\_IPS\_扫描\_预先**属性。

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
<td><p>WIA_SCAN_AHEAD_DISABLED</p></td>
<td><p>继续扫描已禁用。 如果支持该属性，这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SCAN_AHEAD_ENABLED</p></td>
<td><p>已启用继续扫描。 WIA 客户端应用程序必须下载速度一样快，可使用的映像。 如果扫描作业已取消在完成之前，一些扫描的文档可能会丢失 （尚不支持传输到应用程序）。</p></td>
</tr>
</tbody>
</table>

 

此属性是仅对送纸器项有效 (WIA\_类别\_送纸器) 和是可选的。

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

## <a name="see-also"></a>请参阅


[**WIA\_DPS\_SCAN\_AHEAD\_PAGES**](wia-dps-scan-ahead-pages.md)

 

 






