---
title: 用于流式传输类微型驱动程序通信的 DirectShow 筛选器
description: 用于流式传输类微型驱动程序通信的 DirectShow 筛选器
ms.assetid: d2122827-758c-4557-b2fd-8774179b5da4
keywords:
- 筛选器关系图配置 WDK 视频捕获，DirectShow
- DirectShow WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d63a51740bf9ca20f9e690cea5d9e6d6dc4f12c5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105174"
---
# <a name="directshow-filter-to-stream-class-minidriver-communication"></a>用于流式传输类微型驱动程序通信的 DirectShow 筛选器


用户模式 DirectShow 筛选器使用 Win32 API **DeviceIoControl** 函数调用与视频捕获微型驱动程序交互。 流类接口将这些调用转换为流请求块 (SRBs) ，然后将其发送到视频捕获微型驱动程序进行处理。 有两类 SRBs： SRBs 用于常规设备级别控制，以及影响单个流的 SRBs。 下表显示了每个类别的主要 SRBs。

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
<th>Stream</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Property</p>
<div>
 
</div>
写入</td>
<td><p><a href="/windows-hardware/drivers/stream/srb-set-device-property" data-raw-source="[&lt;strong&gt;SRB_SET_DEVICE_PROPERTY&lt;/strong&gt;](./srb-set-device-property.md)"><strong>SRB_SET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/stream/srb-set-stream-property" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_PROPERTY&lt;/strong&gt;](./srb-set-stream-property.md)"><strong>SRB_SET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="even">
<td><p>Property</p>
<div>
 
</div>
读取</td>
<td><p><a href="/windows-hardware/drivers/stream/srb-get-device-property" data-raw-source="[&lt;strong&gt;SRB_GET_DEVICE_PROPERTY&lt;/strong&gt;](./srb-get-device-property.md)"><strong>SRB_GET_DEVICE_PROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/stream/srb-get-stream-property" data-raw-source="[&lt;strong&gt;SRB_GET_STREAM_PROPERTY&lt;/strong&gt;](./srb-get-stream-property.md)"><strong>SRB_GET_STREAM_PROPERTY</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>Stream</p>
<div>
 
</div>
写入</td>
<td><p>无</p></td>
<td><p><a href="/windows-hardware/drivers/stream/srb-write-data" data-raw-source="[&lt;strong&gt;SRB_WRITE_DATA&lt;/strong&gt;](./srb-write-data.md)"><strong>SRB_WRITE_DATA</strong></a></p></td>
</tr>
<tr class="even">
<td><p>Stream</p>
<div>
 
</div>
读取</td>
<td><p>无</p></td>
<td><p><a href="/windows-hardware/drivers/stream/srb-read-data" data-raw-source="[&lt;strong&gt;SRB_READ_DATA&lt;/strong&gt;](./srb-read-data.md)"><strong>SRB_READ_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>打开</p>
<div>
 
</div>
Stream</td>
<td><p><a href="/windows-hardware/drivers/stream/srb-open-stream" data-raw-source="[&lt;strong&gt;SRB_OPEN_STREAM&lt;/strong&gt;](./srb-open-stream.md)"><strong>SRB_OPEN_STREAM</strong></a></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>关闭</p>
<div>
 
</div>
Stream</td>
<td><p><a href="/windows-hardware/drivers/stream/srb-close-stream" data-raw-source="[&lt;strong&gt;SRB_CLOSE_STREAM&lt;/strong&gt;](./srb-close-stream.md)"><strong>SRB_CLOSE_STREAM</strong></a></p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>创建</p>
<div>
 
</div>
格式</td>
<td><p><a href="/windows-hardware/drivers/stream/srb-get-data-intersection" data-raw-source="[&lt;strong&gt;SRB_GET_DATA_INTERSECTION&lt;/strong&gt;](./srb-get-data-intersection.md)"><strong>SRB_GET_DATA_INTERSECTION</strong></a></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>更改</p>
<div>
 
</div>
Stream
<div>
 
</div>
状态</td>
<td><p>无</p></td>
<td><p><a href="/windows-hardware/drivers/stream/srb-set-stream-state" data-raw-source="[&lt;strong&gt;SRB_SET_STREAM_STATE&lt;/strong&gt;](./srb-set-stream-state.md)"><strong>SRB_SET_STREAM_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

对于构成视频捕获筛选器图形的 "前端" 的筛选器，例如视频捕获筛选器、电视/广播调谐器筛选器、电视音频筛选器和十字形筛选器，只有视频捕获筛选器确实参与内核流式处理。 其他筛选器用于控制视频捕获微型驱动程序本身中的设备级属性集。 因此，支持电视/无线电调谐、电视音频和 crossbars 的微型驱动程序不会为其每个流公开内核 pin。 这些流仅作为用户模式构造存在，以创建图形拓扑。

