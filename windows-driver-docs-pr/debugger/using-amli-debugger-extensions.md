---
title: 使用 AMLI 调试器扩展
description: 使用 AMLI 调试器扩展
keywords:
- AMLI 调试器，AMLI 调试器扩展
- amli 扩展
- acpikd. amli 扩展
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: cde0750654ac8713fe9349a1f6576655ba100708
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803167"
---
# <a name="using-amli-debugger-extensions"></a>使用 AMLI 调试器扩展


## <span id="ddk_using_amli_debugger_extensions_dbg"></span><span id="DDK_USING_AMLI_DEBUGGER_EXTENSIONS_DBG"></span>


AMLI 调试器扩展命令包含在扩展模块 Kdexts.dll 中，并使用以下语法：

```dbgcmd
kd> !amli command [parameters] 
```


与任何扩展模块一样，在加载后，可以省略 **acpikd** 前缀。

如果在 AMLI 调试器提示符下，只需输入 *命令* 名称，而无需使用 **！ AMLI** 前缀，即可执行以下任一扩展命令：

```dbgcmd
AMLI(? for help)-> command [parameters] 
```

如果出现此提示，则 **！ amli 调试程序** 命令 (不可用，因为它) 没有任何意义。 此外，帮助命令 ( **？** 在此提示符下 ) 显示所有 AMLI 调试器扩展和命令，而 **！ AMLI？** 扩展只显示有关实际扩展的帮助。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left">Extension 命令</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>显示帮助</p></td>
<td align="left"><p><strong><a href="-amli--.md" data-raw-source="[!amli ?](-amli--.md)">!amli ?</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>设置 AML 断点</p></td>
<td align="left"><p><strong><a href="-amli-bp.md" data-raw-source="[!amli bp](-amli-bp.md)">!amli bp</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>列出 AML 断点</p></td>
<td align="left"><p><strong><a href="-amli-bl.md" data-raw-source="[!amli bl](-amli-bl.md)">!amli bl</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>禁用 AML 断点</p></td>
<td align="left"><p><strong><a href="-amli-bd.md" data-raw-source="[!amli bd](-amli-bd.md)">!amli bd</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>启用 AML 断点</p></td>
<td align="left"><p><strong><a href="-amli-be.md" data-raw-source="[!amli be](-amli-be.md)">!amli be</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>清除 AML 断点</p></td>
<td align="left"><p><strong><a href="-amli-bc.md" data-raw-source="[!amli bc](-amli-bc.md)">!amli bc</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>输入 AMLI 调试器</p></td>
<td align="left"><p><strong><a href="-amli-debugger.md" data-raw-source="[!amli debugger](-amli-debugger.md)">!amli debugger</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>显示事件日志</p></td>
<td align="left"><p><strong><a href="-amli-dl.md" data-raw-source="[!amli dl](-amli-dl.md)">!amli dl</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>清除事件日志</p></td>
<td align="left"><p><strong><a href="-amli-cl.md" data-raw-source="[!amli cl](-amli-cl.md)">!amli cl</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>显示堆</p></td>
<td align="left"><p><strong><a href="-amli-dh.md" data-raw-source="[!amli dh](-amli-dh.md)">!amli dh</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>显示数据对象</p></td>
<td align="left"><p><strong><a href="-amli-do.md" data-raw-source="[!amli do](-amli-do.md)">!amli do</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>显示堆栈</p></td>
<td align="left"><p><strong><a href="-amli-ds.md" data-raw-source="[!amli ds](-amli-ds.md)">!amli ds</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>显示命名空间对象</p></td>
<td align="left"><p><strong><a href="-amli-dns.md" data-raw-source="[!amli dns](-amli-dns.md)">!amli dns</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>查找命名空间对象</p></td>
<td align="left"><p><strong><a href="-amli-find.md" data-raw-source="[!amli find](-amli-find.md)">!amli find</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>显示最接近的方法</p></td>
<td align="left"><p><strong><a href="-amli-ln.md" data-raw-source="[!amli ln](-amli-ln.md)">!amli ln</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>列出所有上下文</p></td>
<td align="left"><p><strong><a href="-amli-lc.md" data-raw-source="[!amli lc](-amli-lc.md)">!amli lc</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>显示上下文信息</p></td>
<td align="left"><p><strong><a href="-amli-r.md" data-raw-source="[!amli r](-amli-r.md)">!amli r</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>Unassemble AML 代码</p></td>
<td align="left"><p><strong><a href="-amli-u.md" data-raw-source="[!amli u](-amli-u.md)">!amli u</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>设置 AMLI 调试器选项</p></td>
<td align="left"><p><strong><a href="-amli-set.md" data-raw-source="[!amli set](-amli-set.md)">!amli set</a></strong></p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[AMLI 调试器](the-amli-debugger.md)
