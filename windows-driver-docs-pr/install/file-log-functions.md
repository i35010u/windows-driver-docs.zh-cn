---
title: 文件的 Log 函数
description: 文件的 Log 函数
ms.assetid: 7d9fe4c9-834f-4dcc-a216-dc6a98ee2fd3
keywords:
- 安装程序 Api 函数 WDK，日志文件
- 日志文件 WDK SetupAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 675e7593dbd47703b7881ca9320bf4aea8f7d7bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541508"
---
# <a name="file-log-functions"></a>文件的 Log 函数





可以使用日志文件来记录有关在安装过程中复制到系统文件的信息。 日志文件可以是系统日志或你自己的安装日志文件。

下表列出了可用于处理日志文件的函数。 函数说明的详细信息，请参阅[Microsoft Windows SDK 文档](https://go.microsoft.com/fwlink/p/?linkid=131248)。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377397" data-raw-source="[&lt;strong&gt;SetupInitializeFileLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377397)"><strong>SetupInitializeFileLog</strong></a></p></td>
<td align="left"><p>初始化用于日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377405" data-raw-source="[&lt;strong&gt;SetupLogError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377405)"><strong>SetupLogError</strong></a></p></td>
<td align="left"><p>将一条错误消息写入到日志文件。 （它应仅安装过程中使用的操作系统。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377406" data-raw-source="[&lt;strong&gt;SetupLogFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377406)"><strong>SetupLogFile</strong></a></p></td>
<td align="left"><p>将条目添加到日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377415" data-raw-source="[&lt;strong&gt;SetupQueryFileLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377415)"><strong>SetupQueryFileLog</strong></a></p></td>
<td align="left"><p>从日志文件中检索信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377429" data-raw-source="[&lt;strong&gt;SetupRemoveFileLogEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377429)"><strong>SetupRemoveFileLogEntry</strong></a></p></td>
<td align="left"><p>从日志文件中删除条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/desktop/aa377443" data-raw-source="[&lt;strong&gt;SetupTerminateFileLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa377443)"><strong>SetupTerminateFileLog</strong></a></p></td>
<td align="left"><p>释放分配给日志文件的资源。</p></td>
</tr>
</tbody>
</table>

 

 

 





