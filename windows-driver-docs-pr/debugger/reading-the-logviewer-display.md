---
title: 阅读 LogViewer 显示内容
description: 阅读 LogViewer 显示内容
keywords:
- LogViewer，显示
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d2039e988c880f8ad319d4a6b28310f58a8f67e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825787"
---
# <a name="reading-the-logviewer-display"></a>阅读 LogViewer 显示内容


## <span id="ddk_reading_the_logviewer_display_dtoolq"></span><span id="DDK_READING_THE_LOGVIEWER_DISPLAY_DTOOLQ"></span>


LogViewer 按记录的顺序显示所有函数的列表。

显示的每一行都包含多个列。 每个列的重要性如下所示。

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
<td align="left"><p>如果此列包含 "+" (加号) ，则指示该函数采用一个或多个参数。 若要查看参数及其值，请双击行或按下向右箭头键，然后按红色显示该行。 若要再次隐藏它，请再次双击它，或在以红色勾勒出行时单击向左箭头键。</p>
<p>此列中也有一个 "d #" 值。 这表示函数调用的 "深度" (，换言之，调用) 的其他已记录函数调用中嵌套的深度。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>函数调用的顺序行号。 如果应用了筛选器，并且想要了解两个函数调用之间相隔多远，这会很有用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Thrd</strong></p></td>
<td align="left"><p>进行函数调用的线程号。 此数字不是线程 ID，而是根据在进程中创建线程的顺序分配的数字。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>呼叫</strong></p></td>
<td align="left"><p>发出函数调用的指令地址。 这是从调用的返回地址派生的。 实际上，返回地址减去5个字节 (<strong>调用 dword ptr</strong> 指令) 的典型大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>模块</strong></p></td>
<td align="left"><p>包含调用指令的模块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>API 函数</strong></p></td>
<td align="left"><p>函数名。 为简洁起见，省略了包含函数的模块的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>返回值</strong></p></td>
<td align="left"><p>函数返回的值（如果它不是 void 函数）。</p></td>
</tr>
</tbody>
</table>

 

双击查看器中的某一行将展开该行，以便向函数显示函数的参数及其值 "进入"。 如果将它们指定为 OUT 参数，则其值将显示在右侧。

你还可以使用 ENTER 键或右箭头键和向左键来展开和折叠行。

返回失败状态代码的函数调用以粉红色灰显。

 

 





