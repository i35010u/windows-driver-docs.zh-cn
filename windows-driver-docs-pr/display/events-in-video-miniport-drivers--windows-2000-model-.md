---
title: 视频微型端口驱动程序中的事件（Windows 2000 模型）
description: 视频微型端口驱动程序中的事件（Windows 2000 模型）
ms.assetid: f6b5ded8-ddb4-4242-9bd3-b12dc96d8f6b
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，事件
- 事件 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f3c70d2f060e3c23cb8f625b8635798a63d209
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383730"
---
# <a name="events-in-video-miniport-drivers-windows-2000-model"></a>视频微型端口驱动程序中的事件（Windows 2000 模型）


## <span id="ddk_events_in_video_miniport_drivers_windows_2000_model__gg"></span><span id="DDK_EVENTS_IN_VIDEO_MINIPORT_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


视频端口驱动程序提供的事件，一种类型的支持[内核调度程序对象](https://msdn.microsoft.com/library/windows/hardware/ff553202)可用于同步调度正在运行的两个线程\_级别。 微型端口驱动程序可以使用事件对视频硬件访问进行同步：

-   通过视频微型端口驱动程序并显示驱动程序

-   显示或视频微型端口驱动程序和另一个组件，例如 OpenGL 驱动程序或程序扩展名 （如控制面板中显示程序）。

下表列出了视频端口驱动程序提供与事件相关的函数。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570284" data-raw-source="[&lt;strong&gt;VideoPortClearEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570284)"><strong>VideoPortClearEvent</strong></a></p></td>
<td align="left"><p>将给定的事件对象设置为非终止状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570287" data-raw-source="[&lt;strong&gt;VideoPortCreateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570287)"><strong>VideoPortCreateEvent</strong></a></p></td>
<td align="left"><p>创建一个事件对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570292" data-raw-source="[&lt;strong&gt;VideoPortDeleteEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570292)"><strong>VideoPortDeleteEvent</strong></a></p></td>
<td align="left"><p>删除指定的事件对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570352" data-raw-source="[&lt;strong&gt;VideoPortReadStateEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570352)"><strong>VideoPortReadStateEvent</strong></a></p></td>
<td align="left"><p>返回给定的事件对象的当前状态： 已发出信号或非终止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570364" data-raw-source="[&lt;strong&gt;VideoPortSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570364)"><strong>VideoPortSetEvent</strong></a></p></td>
<td align="left"><p>设置为终止状态的事件对象，如果它已不处于该状态，并返回事件对象的以前的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570378" data-raw-source="[&lt;strong&gt;VideoPortWaitForSingleObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570378)"><strong>VideoPortWaitForSingleObject</strong></a></p></td>
<td align="left"><p>使当前线程进入等待状态，给定的调度对象设置为终止状态之前或 （可选） 之前等待超时。</p></td>
</tr>
</tbody>
</table>

 

GDI 还提供了查看事件，以显示驱动程序的支持。 请参阅[显示器驱动程序中使用事件](using-events-in-display-drivers.md)有关详细信息。

在事件上更广泛的角度看，请参阅[事件对象](https://msdn.microsoft.com/library/windows/hardware/ff544323)中*内核模式驱动程序设计指南*。

 

 





