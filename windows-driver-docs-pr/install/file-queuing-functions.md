---
title: 文件排队函数
description: 文件排队函数
keywords:
- Setupapi.log 函数 WDK，文件队列
- 文件队列 WDK Setupapi.log
- 队列文件 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d860d8dfabe7e5e1db3b42c355bbfa6f8af17f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828677"
---
# <a name="file-queuing-functions"></a>文件排队函数





使用常规安装函数，可以对文件进行排队以进行各种操作。 可以建立文件队列来复制、重命名和删除文件。 通常，应用程序会将整个安装所需的所有文件操作排队，然后 "提交" 队列，以便在单个批处理中执行这些操作。

下表提供了文件队列功能的摘要。 有关详细的函数说明，请参阅 Microsoft Windows SDK 文档。

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
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupclosefilequeue" data-raw-source="[&lt;strong&gt;SetupCloseFileQueue&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupclosefilequeue)"><strong>SetupCloseFileQueue</strong></a></p></td>
<td align="left"><p>销毁文件队列，以及任何未提交的文件操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupcommitfilequeuea" data-raw-source="[&lt;strong&gt;SetupCommitFileQueue&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupcommitfilequeuea)"><strong>SetupCommitFileQueue</strong></a></p></td>
<td align="left"><p>提交 (执行) 所有已排队操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupopenfilequeue" data-raw-source="[&lt;strong&gt;SetupOpenFileQueue&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupopenfilequeue)"><strong>SetupOpenFileQueue</strong></a></p></td>
<td align="left"><p>创建并返回文件队列的句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setuppromptreboot" data-raw-source="[&lt;strong&gt;SetupPromptReboot&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setuppromptreboot)"><strong>SetupPromptReboot</strong></a></p></td>
<td align="left"><p>如果需要，则提示用户重新启动其计算机。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuecopya" data-raw-source="[&lt;strong&gt;SetupQueueCopy&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuecopya)"><strong>SetupQueueCopy</strong></a></p></td>
<td align="left"><p>对指定文件进行排队以进行复制。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuecopyindirecta" data-raw-source="[&lt;strong&gt;SetupQueueCopyIndirect&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuecopyindirecta)"><strong>SetupQueueCopyIndirect</strong></a></p></td>
<td align="left"><p>对指定文件进行排队以进行复制，并提供文件位置和安全信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuecopysectiona" data-raw-source="[&lt;strong&gt;SetupQueueCopySection&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuecopysectiona)"><strong>SetupQueueCopySection</strong></a></p></td>
<td align="left"><p>对指定 INF 文件部分中的文件进行排队以进行复制。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuedefaultcopya" data-raw-source="[&lt;strong&gt;SetupQueueDefaultCopy&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuedefaultcopya)"><strong>SetupQueueDefaultCopy</strong></a></p></td>
<td align="left"><p>使用 INF 文件中包含的默认源和目标设置，对指定文件进行排队以进行复制。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuedeletea" data-raw-source="[&lt;strong&gt;SetupQueueDelete&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuedeletea)"><strong>SetupQueueDelete</strong></a></p></td>
<td align="left"><p>为要删除的指定文件排队。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuedeletesectiona" data-raw-source="[&lt;strong&gt;SetupQueueDeleteSection&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuedeletesectiona)"><strong>SetupQueueDeleteSection</strong></a></p></td>
<td align="left"><p>对 INF 文件部分中的文件进行排队以进行删除。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuerenamea" data-raw-source="[&lt;strong&gt;SetupQueueRename&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuerenamea)"><strong>SetupQueueRename</strong></a></p></td>
<td align="left"><p>对指定文件进行排队以进行重命名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupqueuerenamesectiona" data-raw-source="[&lt;strong&gt;SetupQueueRenameSection&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupqueuerenamesectiona)"><strong>SetupQueueRenameSection</strong></a></p></td>
<td align="left"><p>对 INF 部分中的文件进行排队以进行重命名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupscanfilequeuea" data-raw-source="[&lt;strong&gt;SetupScanFileQueue&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupscanfilequeuea)"><strong>SetupScanFileQueue</strong></a></p></td>
<td align="left"><p>扫描文件队列，并对每个队列项执行指定的操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupsetplatformpathoverridea" data-raw-source="[&lt;strong&gt;SetupSetPlatformPathOverride&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupsetplatformpathoverridea)"><strong>SetupSetPlatformPathOverride</strong></a></p></td>
<td align="left"><p>设置用于重写默认平台特定源路径的值。</p></td>
</tr>
</tbody>
</table>

 

