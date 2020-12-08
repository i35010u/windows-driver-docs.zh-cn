---
title: GDI 信息服务
description: GDI 信息服务
keywords:
- GDI WDK Windows 2000 显示，信息服务
- 图形驱动程序 WDK Windows 2000 显示，信息服务
- 绘制 WDK GDI，信息服务
- 时间戳 WDK GDI
- 计数器 WDK GDI
- 性能计数器 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12345fbb310cfc3edd711aef0394ffe29647dec3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783269"
---
# <a name="gdi-information-services"></a>GDI 信息服务


## <span id="ddk_gdi_information_services_gg"></span><span id="DDK_GDI_INFORMATION_SERVICES_GG"></span>


GDI 提供若干服务，驱动程序可以使用这些服务在系统中查询设备和系统属性、文件的时间戳和性能计数器。 下表列出了这些服务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engquerydeviceattribute" data-raw-source="[&lt;strong&gt;EngQueryDeviceAttribute&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engquerydeviceattribute)"><strong>EngQueryDeviceAttribute</strong></a></p></td>
<td align="left"><p>允许驱动程序在系统中查询设备的特定属性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engqueryfiletimestamp" data-raw-source="[&lt;strong&gt;EngQueryFileTimeStamp&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engqueryfiletimestamp)"><strong>EngQueryFileTimeStamp</strong></a></p></td>
<td align="left"><p>返回文件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engquerylocaltime" data-raw-source="[&lt;strong&gt;EngQueryLocalTime&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engquerylocaltime)"><strong>EngQueryLocalTime</strong></a></p></td>
<td align="left"><p>查询本地时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engqueryperformancecounter" data-raw-source="[&lt;strong&gt;EngQueryPerformanceCounter&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engqueryperformancecounter)"><strong>EngQueryPerformanceCounter</strong></a></p></td>
<td align="left"><p>查询性能计数器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engqueryperformancefrequency" data-raw-source="[&lt;strong&gt;EngQueryPerformanceFrequency&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engqueryperformancefrequency)"><strong>EngQueryPerformanceFrequency</strong></a></p></td>
<td align="left"><p>查询性能计数器的频率。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engquerysystemattribute" data-raw-source="[&lt;strong&gt;EngQuerySystemAttribute&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engquerysystemattribute)"><strong>EngQuerySystemAttribute</strong></a></p></td>
<td align="left"><p>查询处理器或系统特定的功能。</p></td>
</tr>
</tbody>
</table>

 

