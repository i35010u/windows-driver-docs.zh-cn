---
title: 文件日志函数
description: 文件日志函数
ms.assetid: 7d9fe4c9-834f-4dcc-a216-dc6a98ee2fd3
keywords:
- Setupapi.log 函数 WDK，日志文件
- 日志文件 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf59bf1c0bf34e43f0ab7bf726bd84f083bbac04
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095347"
---
# <a name="file-log-functions"></a>文件日志函数





您可以使用日志文件来记录在安装过程中复制到系统的文件的相关信息。 日志文件可以是系统日志，也可以是自己的安装日志文件。

下表列出了可用于操作日志文件的函数。 有关函数说明的详细信息，请参阅 [Microsoft Windows SDK 文档](https://go.microsoft.com/fwlink/p/?linkid=131248)。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupinitializefileloga" data-raw-source="[&lt;strong&gt;SetupInitializeFileLog&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupinitializefileloga)"><strong>SetupInitializeFileLog</strong></a></p></td>
<td align="left"><p>初始化日志文件以供使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuplogerrora" data-raw-source="[&lt;strong&gt;SetupLogError&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setuplogerrora)"><strong>SetupLogError</strong></a></p></td>
<td align="left"><p>将错误消息写入日志文件。  (仅应在操作系统的安装过程中使用它。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setuplogfilea" data-raw-source="[&lt;strong&gt;SetupLogFile&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setuplogfilea)"><strong>SetupLogFile</strong></a></p></td>
<td align="left"><p>将条目添加到日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupqueryfileloga" data-raw-source="[&lt;strong&gt;SetupQueryFileLog&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupqueryfileloga)"><strong>SetupQueryFileLog</strong></a></p></td>
<td align="left"><p>从日志文件中检索信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupremovefilelogentrya" data-raw-source="[&lt;strong&gt;SetupRemoveFileLogEntry&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupremovefilelogentrya)"><strong>SetupRemoveFileLogEntry</strong></a></p></td>
<td align="left"><p>从日志文件中删除条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupterminatefilelog" data-raw-source="[&lt;strong&gt;SetupTerminateFileLog&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupterminatefilelog)"><strong>SetupTerminateFileLog</strong></a></p></td>
<td align="left"><p>释放分配给日志文件的资源。</p></td>
</tr>
</tbody>
</table>

 

 

