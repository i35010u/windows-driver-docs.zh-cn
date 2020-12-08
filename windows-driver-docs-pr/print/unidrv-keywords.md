---
title: Unidrv 关键字
description: Unidrv 关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 965d547f348a9a081938d33eca57604877cbf09b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822733"
---
# <a name="unidrv-keywords"></a>Unidrv 关键字


Unidrv 插件应使用字符串，因为它们显示在 GPD 视图中 (不是配置文件的 GDL 视图) ，用于调用帮助程序接口上的方法。 此外，Unidrv 提供的功能前面有一个百分号 (% ) 。 下表列出了支持的模拟功能。

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
"True"</td>
<td><p>启用 EMF 假脱机。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="even">
<td><p><strong>%PageOrder</strong></p></td>
<td><p>"FrontToBack"</p>
<p>"BackToFront"</p></td>
<td><p>指定页面的打印顺序。</p>
<p>此功能仅在打印处理器能够执行 EMF 假脱机时可用。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PagePerSheet</strong></p></td>
<td><p></p>
"1"、"2"、"4"、6 "、" 9 "、" 16 "、" 手册 "</td>
<td><p>指定在物理页面上打印的逻辑页的数目。 只有定义了双工功能，"手册" 选项才可用。</p>
<p>此功能仅在打印处理器能够执行 EMF 假脱机时可用。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="even">
<td><p><strong>%TextAsGraphics</strong></p></td>
<td><p></p>
"True"</td>
<td><p>将文本打印为图形。</p>
<p>文档-粘滞。</p></td>
</tr>
</tbody>
</table>

 

某些 GPD 语法在分析时展开以创建功能和选项。 属于此类别的最常见语法是 \* **MemConfigKB** 关键字。 其他包括 \* *_MemConfigMB_*、 \* *_MemoryConfigKB_* 和可 \* *_安装_* 关键字。

 

 




