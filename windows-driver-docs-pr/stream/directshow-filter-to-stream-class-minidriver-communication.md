---
title: DirectShow 筛选器添加到 Stream 类微型驱动程序通信
description: DirectShow 筛选器添加到 Stream 类微型驱动程序通信
ms.assetid: d2122827-758c-4557-b2fd-8774179b5da4
keywords:
- 筛选图形配置 WDK 视频捕获，DirectShow
- DirectShow WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c79b4b9634630f6a4972f8733373989808512576
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544801"
---
# <a name="directshow-filter-to-stream-class-minidriver-communication"></a>DirectShow 筛选器添加到 Stream 类微型驱动程序通信


用户模式下 DirectShow 筛选器与视频捕获微型驱动程序使用 Win32 API 交互**DeviceIoControl**函数调用。 这些调用的 Stream 类接口转换为流请求块 (Srb)，然后发送到的视频捕获微型驱动程序处理。 有两种类别的 Srb:Srb 用于常规设备级别的控件，并会影响单个流 Srb。 每个类别主要 Srb 表所示。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>设备</th>
<th>“数据流”，</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>属性</p>
<div>
 
</div>
写入</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568204" data-raw-source="[&lt;strong&gt;SRB_SET_DEVICE_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568204)"><strong>SRB_SET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568207" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568207)"><strong>SRB_SET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="even">
<td><p>属性</p>
<div>
 
</div>
Read</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568170" data-raw-source="[&lt;strong&gt;SRB_GET_DEVICE_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568170)"><strong>SRB_GET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568175" data-raw-source="[&lt;strong&gt;SRB_GET_STREAM_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568175)"><strong>SRB_GET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>“数据流”，</p>
<div>
 
</div>
写入</td>
<td><p>无</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568220" data-raw-source="[&lt;strong&gt;SRB_WRITE_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568220)"><strong>SRB_WRITE_DATA</strong></a></p></td>
</tr>
<tr class="even">
<td><p>“数据流”，</p>
<div>
 
</div>
Read</td>
<td><p>无</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568200" data-raw-source="[&lt;strong&gt;SRB_READ_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568200)"><strong>SRB_READ_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>打开</p>
<div>
 
</div>
“数据流”，</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568191" data-raw-source="[&lt;strong&gt;SRB_OPEN_STREAM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568191)"><strong>SRB_OPEN_STREAM</strong></a></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>关闭</p>
<div>
 
</div>
“数据流”，</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568165" data-raw-source="[&lt;strong&gt;SRB_CLOSE_STREAM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568165)"><strong>SRB_CLOSE_STREAM</strong></a></p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>创建</p>
<div>
 
</div>
格式</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568168" data-raw-source="[&lt;strong&gt;SRB_GET_DATA_INTERSECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568168)"><strong>SRB_GET_DATA_INTERSECTION</strong></a></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>“更改”</p>
<div>
 
</div>
“数据流”，
<div>
 
</div>
状态</td>
<td><p>无</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568210" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568210)"><strong>SRB_SET_STREAM_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

构成的"前端"视频捕获筛选器关系图，如视频捕获筛选器、 电视/广播调谐器筛选器、 电视音频筛选器和纵横制筛选器的筛选器的视频捕获筛选器真正参与内核流式处理。 其他筛选器用于控制视频捕获微型驱动程序本身中的设备级别的属性集。 因此，支持电视/单选优化、 电视音频和纵横制的微型驱动程序不会为每个其流公开内核 pin。 这些流仅存在于用户模式构造来创建图形拓扑。

 

 




