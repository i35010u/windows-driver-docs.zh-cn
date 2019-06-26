---
title: GDI 信息服务
description: GDI 信息服务
ms.assetid: f3575d68-1d90-4ccd-adb1-5d2a26099397
keywords:
- GDI WDK Windows 2000 显示，信息服务
- 图形驱动程序 WDK Windows 2000 显示，信息服务
- 绘制 WDK GDI，信息服务
- WDK GDI 进行时间戳
- 计数器 WDK GDI
- WDK GDI 的性能计数器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fd354aada1586db1ae38240512eec17c7d2a035
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354738"
---
# <a name="gdi-information-services"></a>GDI 信息服务


## <span id="ddk_gdi_information_services_gg"></span><span id="DDK_GDI_INFORMATION_SERVICES_GG"></span>


GDI 提供驱动程序可用于查询系统的有关设备和系统属性、 文件的时间戳和性能计数器的多个服务。 在下表列出这些服务。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerydeviceattribute" data-raw-source="[&lt;strong&gt;EngQueryDeviceAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerydeviceattribute)"><strong>EngQueryDeviceAttribute</strong></a></p></td>
<td align="left"><p>允许查询有关特定属性系统中的设备驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engqueryfiletimestamp" data-raw-source="[&lt;strong&gt;EngQueryFileTimeStamp&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engqueryfiletimestamp)"><strong>EngQueryFileTimeStamp</strong></a></p></td>
<td align="left"><p>返回一个文件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerylocaltime" data-raw-source="[&lt;strong&gt;EngQueryLocalTime&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerylocaltime)"><strong>EngQueryLocalTime</strong></a></p></td>
<td align="left"><p>查询本地时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engqueryperformancecounter" data-raw-source="[&lt;strong&gt;EngQueryPerformanceCounter&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engqueryperformancecounter)"><strong>EngQueryPerformanceCounter</strong></a></p></td>
<td align="left"><p>查询的性能计数器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engqueryperformancefrequency" data-raw-source="[&lt;strong&gt;EngQueryPerformanceFrequency&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engqueryperformancefrequency)"><strong>EngQueryPerformanceFrequency</strong></a></p></td>
<td align="left"><p>查询的性能计数器的频率。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerysystemattribute" data-raw-source="[&lt;strong&gt;EngQuerySystemAttribute&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerysystemattribute)"><strong>EngQuerySystemAttribute</strong></a></p></td>
<td align="left"><p>查询处理器或特定于系统的功能。</p></td>
</tr>
</tbody>
</table>

 

 

 





