---
title: 默认的队列回调常规函数
description: 默认的队列回调常规函数
keywords:
- Setupapi.log 函数 WDK，默认队列回调例程
- 默认队列回调例程
- 队列回调例程 WDK Setupapi.log
- 回调例程 WDK Setupapi.log
- 队列文件 WDK Setupapi.log
- 文件队列 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 614cf3d39b52882eb736d2b4e9e7f1b67992d890
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782909"
---
# <a name="default-queue-callback-routine-functions"></a>默认的队列回调常规函数





如果将回调例程与文件队列相关联，则每次系统执行某个排队的文件操作时，都将调用回调例程。 通常，可以使用默认队列回调例程 [**SetupDefaultQueueCallback**](/windows/win32/api/setupapi/nf-setupapi-setupdefaultqueuecallbacka)来处理这些通知。

下表列出了与默认队列回调例程关联的函数。 有关详细的函数说明，以及有关如何将回调例程用于文件队列的详细信息，请参阅 Microsoft Windows SDK 文档。

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
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupdefaultqueuecallbacka" data-raw-source="[&lt;strong&gt;SetupDefaultQueueCallback&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupdefaultqueuecallbacka)"><strong>SetupDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>处理执行排队文件操作时系统发送的通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupinitdefaultqueuecallback" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallback&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupinitdefaultqueuecallback)"><strong>SetupInitDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>初始化 <strong>SetupDefaultQueueCallback</strong>所需的上下文信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupinitdefaultqueuecallbackex" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallbackEx&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupinitdefaultqueuecallbackex)"><strong>SetupInitDefaultQueueCallbackEx</strong></a></p></td>
<td align="left"><p>初始化 <strong>SetupDefaultQueueCallback</strong>所需的上下文信息，并提供一个单独的窗口用于显示进度消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setuptermdefaultqueuecallback" data-raw-source="[&lt;strong&gt;SetupTermDefaultQueueCallback&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setuptermdefaultqueuecallback)"><strong>SetupTermDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>通知系统 <a href="/windows-hardware/drivers/#wdkgloss-device-installation-application" data-raw-source="&lt;em&gt;device installation application&lt;/em&gt;"><em>设备安装应用程序</em></a> 将不会提交任何其他文件队列操作。</p></td>
</tr>
</tbody>
</table>

 

