---
title: 默认队列回调例程函数
description: 默认队列回调例程函数
ms.assetid: 46d767ed-cfeb-4bd0-8792-08781a1335d6
keywords:
- 安装程序 Api 函数 WDK，默认队列回调例程
- 默认队列回调例程
- 队列回调例程 WDK SetupAPI
- 回调例程 WDK SetupAPI
- 队列文件 WDK SetupAPI
- 文件队列 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da8b6c4d54e6bb8055efc3bdeecd84c5a5909a64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524507"
---
# <a name="default-queue-callback-routine-functions"></a>默认队列回调例程函数





如果将回调例程与文件队列相关联，则将在系统执行排队的文件操作的其中一个每次调用回调例程。 通常情况下，可以使用的默认队列回调例程[ **SetupDefaultQueueCallback**](https://msdn.microsoft.com/library/windows/desktop/aa376993)，以处理这些通知。

下表列出了与默认队列回调例程相关的功能。 有关函数的详细的说明，以及有关如何将回调例程用于文件队列的详细信息，请参阅 Microsoft Windows SDK 文档。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa376993" data-raw-source="[&lt;strong&gt;SetupDefaultQueueCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa376993)"><strong>SetupDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>处理系统排队时发送的通知执行文件操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377395" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377395)"><strong>SetupInitDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>初始化所需的上下文信息<strong>SetupDefaultQueueCallback</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377396" data-raw-source="[&lt;strong&gt;SetupInitDefaultQueueCallbackEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377396)"><strong>SetupInitDefaultQueueCallbackEx</strong></a></p></td>
<td align="left"><p>初始化所需的上下文信息<strong>SetupDefaultQueueCallback</strong>，并提供一个单独的窗口用于显示进度消息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377442" data-raw-source="[&lt;strong&gt;SetupTermDefaultQueueCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377442)"><strong>SetupTermDefaultQueueCallback</strong></a></p></td>
<td align="left"><p>通知系统的<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-device-installation-application" data-raw-source="&lt;em&gt;device installation application&lt;/em&gt;"><em>设备安装应用程序</em></a>提交任何其他文件队列操作将不提交。</p></td>
</tr>
</tbody>
</table>

 

 

 





