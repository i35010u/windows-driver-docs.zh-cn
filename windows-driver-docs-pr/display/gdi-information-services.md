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
ms.openlocfilehash: f7e54bfa34ec8013547431b81fb2851e99fcd7af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569103"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564986" data-raw-source="[&lt;strong&gt;EngQueryDeviceAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564986)"><strong>EngQueryDeviceAttribute</strong></a></p></td>
<td align="left"><p>允许查询有关特定属性系统中的设备驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564988" data-raw-source="[&lt;strong&gt;EngQueryFileTimeStamp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564988)"><strong>EngQueryFileTimeStamp</strong></a></p></td>
<td align="left"><p>返回一个文件的时间戳。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564990" data-raw-source="[&lt;strong&gt;EngQueryLocalTime&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564990)"><strong>EngQueryLocalTime</strong></a></p></td>
<td align="left"><p>查询本地时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564994" data-raw-source="[&lt;strong&gt;EngQueryPerformanceCounter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564994)"><strong>EngQueryPerformanceCounter</strong></a></p></td>
<td align="left"><p>查询的性能计数器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564996" data-raw-source="[&lt;strong&gt;EngQueryPerformanceFrequency&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564996)"><strong>EngQueryPerformanceFrequency</strong></a></p></td>
<td align="left"><p>查询的性能计数器的频率。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564997" data-raw-source="[&lt;strong&gt;EngQuerySystemAttribute&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564997)"><strong>EngQuerySystemAttribute</strong></a></p></td>
<td align="left"><p>查询处理器或特定于系统的功能。</p></td>
</tr>
</tbody>
</table>

 

 

 





