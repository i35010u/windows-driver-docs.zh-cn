---
title: lse（启动源编辑器）
description: Lse 命令为当前源文件打开编辑器。
keywords:
- lse (启动源编辑器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lse (Launch Source Editor)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fdf44a60e31c4fb4a4174697e73ae309c5396d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783444"
---
# <a name="lse-launch-source-editor"></a>lse（启动源编辑器）


**Lse** 命令为当前源文件打开编辑器。

```dbgcmd
lse 
```

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Lse** 命令为当前源文件打开编辑器。 此命令等效于在 WinDbg 的 [源窗口](source-window.md)的快捷菜单中单击 "**编辑此文件**"。

编辑器将在运行目标的计算机上打开，因此不能从远程客户端使用 **lse** 命令。

WinDiff 编辑器注册表信息或 WINDBG \_ INVOKE \_ editor 环境变量的值确定打开的编辑器。 例如，请考虑 WINDBG 调用编辑器的以下 \_ 值 \_ 。

```reg
c:\my\path\myeditor.exe -file %f -line %l
```

此值指示 Myeditor.exe 将打开到当前源文件的从1开始的行号。 **% L** 选项指示行号应作为一开始读取， **% f** 指示应使用当前源文件。 您还可以包含 **% L** ，以指示行号是从零开始的，或者是 **% p** 以指示应使用当前源文件。

 

 





