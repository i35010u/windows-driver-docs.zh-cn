---
title: 使用显示驱动程序中的事件
description: 使用显示驱动程序中的事件
ms.assetid: 0c02d64f-0aad-43b4-b105-09ab8901e0de
keywords:
- 显示事件 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36c08bb5b9e0d677f45f0c2f76338e3f49b6cfa6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370645"
---
# <a name="using-events-in-display-drivers"></a>使用显示驱动程序中的事件


## <span id="ddk_using_events_in_display_drivers_gg"></span><span id="DDK_USING_EVENTS_IN_DISPLAY_DRIVERS_GG"></span>


GDI 提供事件，一种类型的支持[内核调度程序对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/kernel-dispatcher-objects)可用于同步调度正在运行的两个线程\_级别。 显示驱动程序可以使用事件对视频硬件访问进行同步：

-   通过显示驱动程序和视频的微型端口驱动程序

-   显示或视频微型端口驱动程序和另一个组件，例如 OpenGL 驱动程序或程序扩展名 （如控制面板中显示程序）。

下表列出了与 GDI 与事件相关的函数。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engclearevent" data-raw-source="[&lt;strong&gt;EngClearEvent&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engclearevent)"><strong>EngClearEvent</strong></a></p></td>
<td align="left"><p>将给定的事件对象设置为非终止状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateevent" data-raw-source="[&lt;strong&gt;EngCreateEvent&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateevent)"><strong>EngCreateEvent</strong></a></p></td>
<td align="left"><p>创建一个同步事件对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteevent" data-raw-source="[&lt;strong&gt;EngDeleteEvent&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeleteevent)"><strong>EngDeleteEvent</strong></a></p></td>
<td align="left"><p>删除指定的事件对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapevent" data-raw-source="[&lt;strong&gt;EngMapEvent&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapevent)"><strong>EngMapEvent</strong></a></p></td>
<td align="left"><p>将用户模式事件对象映射到内核模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engreadstateevent" data-raw-source="[&lt;strong&gt;EngReadStateEvent&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engreadstateevent)"><strong>EngReadStateEvent</strong></a></p></td>
<td align="left"><p>返回给定的事件对象的当前状态： 已发出信号或非终止。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetevent" data-raw-source="[&lt;strong&gt;EngSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetevent)"><strong>EngSetEvent</strong></a></p></td>
<td align="left"><p>设置为终止状态的事件对象，如果它已不处于该状态，并返回事件对象的以前的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapevent" data-raw-source="[&lt;strong&gt;EngUnmapEvent&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapevent)"><strong>EngUnmapEvent</strong></a></p></td>
<td align="left"><p>清理为映射的用户模式事件分配的内核模式资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwaitforsingleobject" data-raw-source="[&lt;strong&gt;EngWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwaitforsingleobject)"><strong>EngWaitForSingleObject</strong></a></p></td>
<td align="left"><p>使当前线程进入等待状态，给定的调度对象设置为终止状态之前或 （可选） 之前等待超时。</p></td>
</tr>
</tbody>
</table>

 

视频端口驱动程序还提供对事件到视频的微型端口驱动程序的支持。 请参阅[视频微型端口驱动程序 （Windows 2000 模式） 中的事件](events-in-video-miniport-drivers--windows-2000-model-.md)有关详细信息。

在事件上更广泛的角度看，请参阅[事件对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/event-objects)。

 

 





