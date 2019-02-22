---
title: 读取日志查看器显示
description: 读取日志查看器显示
ms.assetid: 425aff5d-780e-4600-a43a-8012d70263f1
keywords:
- 日志查看器显示
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22f830e62284a3ff7eca0c407561a00a9ae4a699
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547772"
---
# <a name="reading-the-logviewer-display"></a>读取日志查看器显示


## <span id="ddk_reading_the_logviewer_display_dtoolq"></span><span id="DDK_READING_THE_LOGVIEWER_DISPLAY_DTOOLQ"></span>


日志查看器中记录的顺序显示所有函数的列表。

显示的每一行都包含多个列。 每个列的意义是，如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>+/-</strong></p></td>
<td align="left"><p>如果此列包含&quot; + &quot; （加号），它指示该函数采用一个或多个参数。 若要查看参数和它们的值，请双击的行或按向右箭头键，行的边框为红色时。 若要再次隐藏，请双击试或按向左的箭头键时行的边框为红色。</p>
<p>此外，还有&quot;d #&quot;此列中的值。 这表明&quot;深度&quot;函数的调用 （换句话说，深度调用嵌套在其他记录的函数调用中）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>函数调用的顺序的行数。 这是有用的在将筛选器应用并有兴趣知道距离相隔两个函数调用时，是。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Thrd</strong></p></td>
<td align="left"><p>在其进行函数调用的线程数。 此数字不是一个线程 ID，但而不是分配的数字基于在进程中已创建线程的顺序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Caller</strong></p></td>
<td align="left"><p>指令地址，进行调用的函数。 这被派生自调用的返回地址。 它是实际的返回地址减去 5 个字节 (典型的大小<strong>调用 dword ptr</strong>指令)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>模块</strong></p></td>
<td align="left"><p>包含调用指令的模块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>API 函数</strong></p></td>
<td align="left"><p>函数的名称。 为简便起见，已省略包含函数的模块的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>返回值</strong></p></td>
<td align="left"><p>如果不是 void 函数的函数，返回的值。</p></td>
</tr>
</tbody>
</table>

 

双击查看器中的行，将展开以显示该函数，它们的值"将"函数的参数的行。 如果它们被指定为输出参数，在右侧显示"推出"其值。

此外可以使用 ENTER 键或左右箭头键可展开和折叠行。

返回状态代码的失败的函数调用以粉色突出显示以阴影显示。

 

 





