---
title: Unidrv 关键字
description: Unidrv 关键字
ms.assetid: b76fcf53-cd75-4e85-a7a2-00a69cc82a97
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9a3993bfffed8d4437df2cff7d5e419e04abd73
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464247"
---
# <a name="unidrv-keywords"></a>Unidrv 关键字


Unidrv 插件应使用字符串，因为它们出现在方法调用帮助程序接口上的配置文件的 GPD 视图 （而不是 GDL 视图）。 此外，提供 Unidrv 功能都以百分号 （%）。 下表列出了支持的模拟的功能。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能名称</th>
<th>选项</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>%MetafileSpooling</td>
<td><p></p>
"True" "False"</td>
<td><p>启用 EMF 后台处理。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="even">
<td><p><strong>%PageOrder</strong></p></td>
<td><p>"FrontToBack"</p>
<p>"BackToFront"</p></td>
<td><p>指定打印页的顺序。</p>
<p>此功能是打印处理器是能够执行 EMF 后台处理才可用。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PagePerSheet</strong></p></td>
<td><p></p>
"1"、"2"、"4"6"，"9"、"16"，"手册"</td>
<td><p>指定一个物理页上打印的逻辑页的数目。 "手册"选项为定义的双工功能才可用。</p>
<p>此功能是打印处理器是能够执行 EMF 后台处理才可用。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="even">
<td><p><strong>%TextAsGraphics</strong></p></td>
<td><p></p>
"True" "False"</td>
<td><p>按图形方式打印文本。</p>
<p>文档粘性。</p></td>
</tr>
</tbody>
</table>

 

某些 GPD 语法进行了扩展在分析时，若要创建功能和选项。 属于此类别的最常用语法是\* **MemConfigKB**关键字。 其他包括\* **MemConfigMB**， \* **MemoryConfigKB**，以及\***可安装**关键字。

 

 




