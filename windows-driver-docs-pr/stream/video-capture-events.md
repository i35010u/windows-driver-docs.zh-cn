---
title: 视频捕获事件
description: 视频捕获事件
keywords:
- 事件 WDK 视频捕获
- KSEVENTSETID_VIDCAPNotify
- 视频捕获事件 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53e2465ad6fd5b9c8b7fdf5783acb4f0cf6d7060
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825315"
---
# <a name="video-capture-events"></a>视频捕获事件


[KSEVENTSETID \_ VIDCAPNotify](./kseventsetid-vidcapnotify.md)事件集包含与调谐器事件相关的事件。 下表描述了属于 KSEVENTSETID \_ VIDCAPNotify 事件集的事件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSEVENTSETID_VIDCAPNotify KS 事件</th>
<th>事件说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksevent-vidcaptosti-ext-trigger" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAPTOSTI_EXT_TRIGGER&lt;/strong&gt;](./ksevent-vidcaptosti-ext-trigger.md)"><strong>KSEVENT_VIDCAPTOSTI_EXT_TRIGGER</strong></a></p></td>
<td><p>当触发视频捕获设备上的按钮时，向已注册的客户端发出信号。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksevent-vidcap-auto-update" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAP_AUTO_UPDATE&lt;/strong&gt;](./ksevent-vidcap-auto-update.md)"><strong>KSEVENT_VIDCAP_AUTO_UPDATE</strong></a></p></td>
<td><p>当属性值更改时向注册的客户端发出信号。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksevent-vidcap-search" data-raw-source="[&lt;strong&gt;KSEVENT_VIDCAP_SEARCH&lt;/strong&gt;](./ksevent-vidcap-search.md)"><strong>KSEVENT_VIDCAP_SEARCH</strong></a></p></td>
<td><p>搜索完成时向注册的客户端发出信号。</p></td>
</tr>
</tbody>
</table>

 

