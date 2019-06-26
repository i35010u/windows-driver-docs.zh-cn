---
title: 磁盘提示和错误处理函数
description: 磁盘提示和错误处理函数
ms.assetid: e1afeeb3-02f0-4570-9910-f948646f07bf
keywords:
- 安装程序 Api 函数 WDK，磁盘提示
- 安装程序 Api 函数 WDK、 错误处理
- 错误 WDK SetupAPI
- 提示 WDK SetupAPI 的磁盘
- 提示磁盘插入 WDK SetupAPI
- 提示 WDK SetupAPI 媒体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30a874724506eeb43fc78cd08b1b9cde79f39e5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375324"
---
# <a name="disk-prompting-and-error-handling-functions"></a>磁盘提示和错误处理函数





可以使用常规的安装程序函数来提示用户插入新的介质，或者处理在复制文件时引发的错误重命名，或删除。

下表列出了对话框提供用于请求安装介质和报告错误的函数。 有关详细的功能描述，请参阅 Microsoft Windows SDK 文档。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcopyerrora" data-raw-source="[&lt;strong&gt;SetupCopyError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupcopyerrora)"><strong>SetupCopyError</strong></a></p></td>
<td align="left"><p>生成一个对话框，通知复制错误的用户。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdeleteerrora" data-raw-source="[&lt;strong&gt;SetupDeleteError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdeleteerrora)"><strong>SetupDeleteError</strong></a></p></td>
<td align="left"><p>生成一个对话框，通知用户删除错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuppromptfordiska" data-raw-source="[&lt;strong&gt;SetupPromptForDisk&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuppromptfordiska)"><strong>SetupPromptForDisk</strong></a></p></td>
<td align="left"><p>生成一个对话框，提示用户输入了安装介质或源的文件位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuprenameerrora" data-raw-source="[&lt;strong&gt;SetupRenameError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuprenameerrora)"><strong>SetupRenameError</strong></a></p></td>
<td align="left"><p>生成一个对话框，通知用户重命名错误。</p></td>
</tr>
</tbody>
</table>

 

 

 





