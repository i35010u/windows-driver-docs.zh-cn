---
title: GDI 事件服务
description: GDI 事件服务
ms.assetid: 966fa3ce-c72c-4b91-9cf7-b789d39e69b5
keywords:
- GDI WDK Windows 2000 显示事件
- 图形驱动程序 WDK Windows 2000 显示事件
- 绘制 WDK GDI，事件
- 事件 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25336d59aa1afab1f6f109346d2d897878621b40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523125"
---
# <a name="gdi-event-services"></a>GDI 事件服务


## <span id="ddk_gdi_event_services_gg"></span><span id="DDK_GDI_EVENT_SERVICES_GG"></span>


GDI 提供与事件相关的多个服务。 使用这些服务的驱动程序可以创建和删除事件、 映射和取消映射事件和读取、 设置和清除事件。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564190" data-raw-source="[&lt;strong&gt;EngClearEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564190)"><strong>EngClearEvent</strong></a></p></td>
<td align="left"><p>将指定的事件对象设置为非终止状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564211" data-raw-source="[&lt;strong&gt;EngCreateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564211)"><strong>EngCreateEvent</strong></a></p></td>
<td align="left"><p>创建可以用于显示驱动程序和视频的微型端口驱动程序之间的硬件访问进行同步的同步事件对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564801" data-raw-source="[&lt;strong&gt;EngDeleteEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564801)"><strong>EngDeleteEvent</strong></a></p></td>
<td align="left"><p>删除指定的事件对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564970" data-raw-source="[&lt;strong&gt;EngMapEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564970)"><strong>EngMapEvent</strong></a></p></td>
<td align="left"><p>将用户模式事件对象映射到内核模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565001" data-raw-source="[&lt;strong&gt;EngReadStateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565001)"><strong>EngReadStateEvent</strong></a></p></td>
<td align="left"><p>返回指定的事件对象的当前状态： 已发出信号或非终止。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565013" data-raw-source="[&lt;strong&gt;EngSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565013)"><strong>EngSetEvent</strong></a></p></td>
<td align="left"><p>将指定的事件对象设置为终止状态，并返回事件对象&#39;s 以前的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565434" data-raw-source="[&lt;strong&gt;EngUnmapEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565434)"><strong>EngUnmapEvent</strong></a></p></td>
<td align="left"><p>清理为映射的用户模式事件分配的内核模式资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565461" data-raw-source="[&lt;strong&gt;EngWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565461)"><strong>EngWaitForSingleObject</strong></a></p></td>
<td align="left"><p>使显示驱动程序的当前线程进入等待状态，直到指定的事件对象设置为终止状态，或等待超时。</p></td>
</tr>
</tbody>
</table>

 

 

 





