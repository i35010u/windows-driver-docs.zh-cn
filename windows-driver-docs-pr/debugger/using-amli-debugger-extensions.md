---
title: 使用 AMLI 调试器扩展
description: 使用 AMLI 调试器扩展
ms.assetid: 98b9cd6e-b2e1-44bd-aff6-376b9cf2daa2
keywords:
- AMLI 调试器，AMLI 调试器扩展
- amli 扩展
- acpikd.amli 扩展
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2405122012154c1a54133e0a5134942496c64fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568010"
---
# <a name="using-amli-debugger-extensions"></a>使用 AMLI 调试器扩展


## <span id="ddk_using_amli_debugger_extensions_dbg"></span><span id="DDK_USING_AMLI_DEBUGGER_EXTENSIONS_DBG"></span>


包含在扩展模块 Kdexts.dll AMLI 调试器扩展命令中，使用以下语法：

```dbgcmd
kd> !amli command [parameters] 
```


因为与任何扩展模块，它已加载之后您可以省略**acpikd**前缀。

如果您是在 AMLI 调试器提示符下，您可以只需输入执行任何这些扩展命令*命令*名称而无需 **！ amli**前缀：

```dbgcmd
AMLI(? for help)-> command [parameters] 
```

在此提示符下，当 **！ amli 调试器**命令将不可用 （因为它是无意义）。 此外，帮助命令 ( **？** ) 在此提示符下显示所有 AMLI 调试器扩展和命令，而 **！ amli？** 扩展仅在实际扩展上显示的帮助。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">操作</th>
<th align="left">扩展命令</th>
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
<td align="left"><p>显示 Namespace 对象</p></td>
<td align="left"><p><strong><a href="-amli-dns.md" data-raw-source="[!amli dns](-amli-dns.md)">!amli dns</a></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>找不到 Namespace 对象</p></td>
<td align="left"><p><strong><a href="-amli-find.md" data-raw-source="[!amli find](-amli-find.md)">!amli find</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>显示最近的方法</p></td>
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
<td align="left"><p>反汇编 AML 代码</p></td>
<td align="left"><p><strong><a href="-amli-u.md" data-raw-source="[!amli u](-amli-u.md)">!amli u</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>设置 AMLI 调试器选项</p></td>
<td align="left"><p><strong><a href="-amli-set.md" data-raw-source="[!amli set](-amli-set.md)">!amli set</a></strong></p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[AMLI 调试器](the-amli-debugger.md)
