---
title: 使用显示驱动程序中的事件
description: 使用显示驱动程序中的事件
ms.assetid: 0c02d64f-0aad-43b4-b105-09ab8901e0de
keywords:
- 事件 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12a5c613dcf4515980b5bd358fc6dd978610a59d
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717570"
---
# <a name="using-events-in-display-drivers"></a>使用显示驱动程序中的事件


## <span id="ddk_using_events_in_display_drivers_gg"></span><span id="DDK_USING_EVENTS_IN_DISPLAY_DRIVERS_GG"></span>


GDI 为事件提供支持，这是一种可用于同步在调度级别下运行的两个线程的 [内核调度程序对象](../kernel/introduction-to-kernel-dispatcher-objects.md) \_ 。 显示驱动程序可以使用事件来同步对视频硬件的访问：

-   由显示器驱动程序和视频微型端口驱动程序

-   通过显示或视频微型端口驱动程序和其他组件（如 OpenGL 驱动程序或程序扩展） (如 "控制面板" 中的 "显示程序") 。

下表列出了与 GDI 事件相关的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engclearevent" data-raw-source="[&lt;strong&gt;EngClearEvent&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engclearevent)"><strong>EngClearEvent</strong></a></p></td>
<td align="left"><p>将给定的事件对象设置为非终止状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreateevent" data-raw-source="[&lt;strong&gt;EngCreateEvent&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreateevent)"><strong>EngCreateEvent</strong></a></p></td>
<td align="left"><p>创建同步事件对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeleteevent" data-raw-source="[&lt;strong&gt;EngDeleteEvent&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeleteevent)"><strong>EngDeleteEvent</strong></a></p></td>
<td align="left"><p>删除指定的事件对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engmapevent" data-raw-source="[&lt;strong&gt;EngMapEvent&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engmapevent)"><strong>EngMapEvent</strong></a></p></td>
<td align="left"><p>将用户模式事件对象映射到内核模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engreadstateevent" data-raw-source="[&lt;strong&gt;EngReadStateEvent&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engreadstateevent)"><strong>EngReadStateEvent</strong></a></p></td>
<td align="left"><p>返回给定事件对象的当前状态： "已终止" 或 "非终止"。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engsetevent" data-raw-source="[&lt;strong&gt;EngSetEvent&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engsetevent)"><strong>EngSetEvent</strong></a></p></td>
<td align="left"><p>如果事件对象尚未处于该状态，则将其设置为 "已终止" 状态，并返回事件对象先前的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunmapevent" data-raw-source="[&lt;strong&gt;EngUnmapEvent&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunmapevent)"><strong>EngUnmapEvent</strong></a></p></td>
<td align="left"><p>清理为映射的用户模式事件分配的内核模式资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engwaitforsingleobject" data-raw-source="[&lt;strong&gt;EngWaitForSingleObject&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engwaitforsingleobject)"><strong>EngWaitForSingleObject</strong></a></p></td>
<td align="left"><p>将当前线程置于等待状态，直到将给定调度对象设置为终止状态，或者 (（可选）) 直到等待超时。</p></td>
</tr>
</tbody>
</table>

 

视频端口驱动程序还提供对视频微型端口驱动程序的事件支持。 有关详细信息，请参阅适用于 [Windows 2000 模型的视频微型端口驱动程序中的事件 () ](events-in-video-miniport-drivers--windows-2000-model-.md) 。

有关事件的更多详细情况，请参阅 [事件对象](../kernel/event-objects.md)。

