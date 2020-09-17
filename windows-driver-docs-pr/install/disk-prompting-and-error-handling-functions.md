---
title: 磁盘提示和错误处理函数
description: 磁盘提示和错误处理函数
ms.assetid: e1afeeb3-02f0-4570-9910-f948646f07bf
keywords:
- Setupapi.log 函数 WDK，磁盘提示
- Setupapi.log 函数 WDK，错误处理
- 错误 WDK Setupapi.log
- 磁盘提示 WDK Setupapi.log
- 提示磁盘插入 WDK Setupapi.log
- 媒体提示 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9ba62da595b910ec5d7fa15b406f6658f99b566
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715924"
---
# <a name="disk-prompting-and-error-handling-functions"></a>磁盘提示和错误处理函数





您可以使用常规安装程序功能来提示用户插入新媒体，或处理在复制、重命名或删除文件时出现的错误。

下表列出了一些函数，这些函数提供用于请求安装介质和报告错误的对话框。 有关详细的函数说明，请参阅 Microsoft Windows SDK 文档。

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
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupcopyerrora" data-raw-source="[&lt;strong&gt;SetupCopyError&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupcopyerrora)"><strong>SetupCopyError</strong></a></p></td>
<td align="left"><p>生成一个对话框，通知用户出现复制错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setupdeleteerrora" data-raw-source="[&lt;strong&gt;SetupDeleteError&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setupdeleteerrora)"><strong>SetupDeleteError</strong></a></p></td>
<td align="left"><p>生成一个对话框，该对话框将通知用户删除错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setuppromptfordiska" data-raw-source="[&lt;strong&gt;SetupPromptForDisk&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setuppromptfordiska)"><strong>SetupPromptForDisk</strong></a></p></td>
<td align="left"><p>生成一个对话框，提示用户输入安装介质或源文件位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/setupapi/nf-setupapi-setuprenameerrora" data-raw-source="[&lt;strong&gt;SetupRenameError&lt;/strong&gt;](/windows/win32/api/setupapi/nf-setupapi-setuprenameerrora)"><strong>SetupRenameError</strong></a></p></td>
<td align="left"><p>生成一个对话框，通知用户重命名错误。</p></td>
</tr>
</tbody>
</table>

 

