---
title: PCL 分隔符页转义代码
description: PCL 分隔符页转义代码
keywords:
- PCL 分隔符页转义代码 WDK PCL XL
- PCL XL 矢量图形 WDK Unidrv，分隔符页转义码
- 转义码 WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cee99e0349dc418ad10aae1a914bf91939ee73f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807619"
---
# <a name="pcl-separator-page-escape-codes"></a>PCL 分隔符页转义代码





在创建 PCL 分隔符页时，可以使用下表中所示的转义码。

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
<td><p>分隔符文件的第一行必须只包含此字符。 分隔符文件解释器以分隔符形式读取分隔符文件命令。</p></td>
</tr>
<tr class="even">
<td><p>&lt;em &gt; n</em></p></td>
<td><p>跳过 <em>n</em> (从0到 9) 指定的行数。 跳过0行将打印移到下一行。</p></td>
</tr>
<tr class="odd">
<td><p>\B\M</p></td>
<td><p>在遇到 \U 之前，将文本打印为全角字符。</p></td>
</tr>
<tr class="even">
<td><p>\B\S</p></td>
<td><p>在遇到 \U 之前，以单宽度块字符打印文本。</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>打印作业的打印日期。 时间以在 "区域选项" 下指定的格式显示， (Windows 2000) 或 "控制面板" 中 (Windows XP 和更高) 版本的 "区域和语言选项"。</p></td>
</tr>
<tr class="even">
<td><p>正规</p></td>
<td><p>从打印机中弹出页面。 使用此代码可启动新的分隔页或结束分隔符页文件。 如果在打印时收到额外的空白分隔页，请从分隔符页文件中删除此代码。</p></td>
</tr>
<tr class="odd">
<td><p>\F<em>路径名</em></p></td>
<td><p>打印 <em>pathname</em>指定的文件的内容，从空行开始。 此文件的内容直接复制到打印机，而不进行处理。</p></td>
</tr>
<tr class="even">
<td><p>\H<em>nn</em></p></td>
<td><p>设置特定于打印机的控件序列，其中 <em>nn</em> 是直接发送到打印机的十六进制 ASCII 代码。 请参阅打印机手册来确定具体的数字。</p></td>
</tr>
<tr class="odd">
<td><p>\I</p></td>
<td><p>打印作业编号。</p></td>
</tr>
<tr class="even">
<td><p>\L<em>xxx</em></p></td>
<td><p>打印 \L 转义代码后显示的文本字符串。 如果输入 \LTest，则 "Test" 文本将显示在 "分隔符" 页中。</p></td>
</tr>
<tr class="odd">
<td><p>\N</p></td>
<td><p>打印作业的提交者的用户名。</p></td>
</tr>
<tr class="even">
<td><p>\U</p></td>
<td><p>关闭阻止字符打印。</p></td>
</tr>
<tr class="odd">
<td><p>\W<em>nn</em></p></td>
<td><p>设置分隔符页的宽度。 默认宽度为80个字符，最大宽度为256个字符。 将删除超出此宽度的字符。</p></td>
</tr>
</tbody>
</table>

 

本地打印提供程序通过打印处理器和分隔页处理器传递作业后，会将作业从后台处理程序发送到相应的端口打印监视器。

 

 




