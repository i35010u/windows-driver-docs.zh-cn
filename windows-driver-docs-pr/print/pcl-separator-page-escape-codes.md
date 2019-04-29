---
title: PCL 分隔符页转义代码
description: PCL 分隔符页转义代码
ms.assetid: 8e571fcd-f6ee-4a56-8d8a-20bf3a5c333c
keywords:
- PCL 分隔符页转义代码 WDK PCL XL
- PCL XL 矢量图形 WDK Unidrv，分隔页转义码
- 转义码 WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef63ceb12b1f08b9367797206a9581d27463917
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390925"
---
# <a name="pcl-separator-page-escape-codes"></a>PCL 分隔符页转义代码





创建 PCL 分隔页时，可以使用下表中所示的转义代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>转义码</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;/p&gt;</td>
<td><p>分隔符文件的第一行必须包含仅此字符。 分隔符文件解释器读取分隔符作为分隔符文件命令。</p></td>
</tr>
<tr class="even">
<td><p>&lt;em&gt;n</em></p></td>
<td><p>将跳过指定的行数<em>n</em> （从 0 到 9)。 正在跳过 0 行，则会将打印移到下一行。</p></td>
</tr>
<tr class="odd">
<td><p>\B\M</p></td>
<td><p>在中打印文本双宽度的块字符直到遇到 \U。</p></td>
</tr>
<tr class="even">
<td><p>\B\S</p></td>
<td><p>在中打印文本单宽度的块字符直到遇到 \U。</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>打印打印作业的日期。 在区域选项 (Windows 2000) 或区域和语言选项下指定的格式显示时间 (Windows XP 及更高版本) 在控制面板中。</p></td>
</tr>
<tr class="even">
<td><p>\E</p></td>
<td><p>弹出来自打印机的页面。 若要启动新的分隔符页或结束分隔符页文件，请使用此代码。 如果在打印时获取额外的空白分隔页，请从分隔符页面文件中删除此代码。</p></td>
</tr>
<tr class="odd">
<td><p>\F<em>pathname</em></p></td>
<td><p>打印指定的文件的内容<em>pathname</em>，从空的行上开始。 此文件的内容是直接复制到的打印机，而无需处理。</p></td>
</tr>
<tr class="even">
<td><p>\H<em>nn</em></p></td>
<td><p>设置特定于打印机的控制序列，其中<em>nn</em>是直接发送到打印机的十六进制 ASCII 代码。 请参阅打印机手册以确定特定的数字。</p></td>
</tr>
<tr class="odd">
<td><p>\I</p></td>
<td><p>打印作业数。</p></td>
</tr>
<tr class="even">
<td><p>\L<em>xxx</em></p></td>
<td><p>打印 \L 转义代码后显示的文本的字符串。 如果输入 \LTest，在分隔符页将显示文本"Test"。</p></td>
</tr>
<tr class="odd">
<td><p>\N</p></td>
<td><p>将打印已提交作业的人员的用户名。</p></td>
</tr>
<tr class="even">
<td><p>\U</p></td>
<td><p>关闭块字符打印。</p></td>
</tr>
<tr class="odd">
<td><p>\W<em>nn</em></p></td>
<td><p>设置分隔符页的宽度。 默认宽度为 80 个字符，并最大宽度为 256 个字符。 超出此宽度的字符将被删除。</p></td>
</tr>
</tbody>
</table>

 

本地打印提供程序通过打印处理器和分隔符页处理器通过作业后，它将发送作业后台处理程序从到适当的端口的打印监视器。

 

 




