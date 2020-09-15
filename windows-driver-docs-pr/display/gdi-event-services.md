---
title: GDI 事件服务
description: GDI 事件服务
ms.assetid: 966fa3ce-c72c-4b91-9cf7-b789d39e69b5
keywords:
- GDI WDK Windows 2000 显示，事件
- 图形驱动程序 WDK Windows 2000 显示，事件
- 绘制 WDK GDI，事件
- 事件 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 435434bbefee1debb6ac9afb88f18f5b48ce92af
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106270"
---
# <a name="gdi-event-services"></a>GDI 事件服务


## <span id="ddk_gdi_event_services_gg"></span><span id="DDK_GDI_EVENT_SERVICES_GG"></span>


GDI 提供了若干与事件相关的服务。 使用这些服务的驱动程序可以创建和删除事件、映射和取消映射事件，以及读取、设置和清除事件。

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
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engclearevent" data-raw-source="[&lt;strong&gt;EngClearEvent&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engclearevent)"><strong>EngClearEvent</strong></a></p></td>
<td align="left"><p>将指定的事件对象设置为非终止状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engcreateevent" data-raw-source="[&lt;strong&gt;EngCreateEvent&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engcreateevent)"><strong>EngCreateEvent</strong></a></p></td>
<td align="left"><p>创建一个同步事件对象，该对象可用于同步显示驱动程序与视频微型端口驱动程序之间的硬件访问。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engdeleteevent" data-raw-source="[&lt;strong&gt;EngDeleteEvent&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engdeleteevent)"><strong>EngDeleteEvent</strong></a></p></td>
<td align="left"><p>删除指定的事件对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engmapevent" data-raw-source="[&lt;strong&gt;EngMapEvent&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engmapevent)"><strong>EngMapEvent</strong></a></p></td>
<td align="left"><p>将用户模式事件对象映射到内核模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engreadstateevent" data-raw-source="[&lt;strong&gt;EngReadStateEvent&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engreadstateevent)"><strong>EngReadStateEvent</strong></a></p></td>
<td align="left"><p>返回指定的事件对象的当前状态：已终止或非终止。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engsetevent" data-raw-source="[&lt;strong&gt;EngSetEvent&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engsetevent)"><strong>EngSetEvent</strong></a></p></td>
<td align="left"><p>将指定的事件对象设置为终止状态，并返回事件对象以前的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engunmapevent" data-raw-source="[&lt;strong&gt;EngUnmapEvent&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engunmapevent)"><strong>EngUnmapEvent</strong></a></p></td>
<td align="left"><p>清理为映射的用户模式事件分配的内核模式资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-engwaitforsingleobject" data-raw-source="[&lt;strong&gt;EngWaitForSingleObject&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-engwaitforsingleobject)"><strong>EngWaitForSingleObject</strong></a></p></td>
<td align="left"><p>将显示驱动程序的当前线程置于等待状态，直到指定的事件对象设置为终止状态，或者直到等待超时。</p></td>
</tr>
</tbody>
</table>

 

