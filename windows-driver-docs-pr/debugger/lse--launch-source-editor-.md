---
title: lse（启动源编辑器）
description: Lse 命令将打开用于当前源文件的编辑器。
ms.assetid: 2f66b5c3-1cd6-4641-8dea-5e3a11c87db0
keywords:
- lse （启动源编辑器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lse (Launch Source Editor)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de740909aff1b6575cbec845a74e75ff2a053f89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383317"
---
# <a name="lse-launch-source-editor"></a>lse（启动源编辑器）


**Lse**命令将打开用于当前源文件的编辑器。

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
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**Lse**命令将打开用于当前源文件的编辑器。 此命令是等效于单击**编辑此文件**中的快捷菜单[源窗口](source-window.md)在 WinDbg 中。

因此不能使用在编辑器，运行目标计算机上打开**lse**命令从远程客户端。

WinDiff 编辑器注册表信息或值的 WINDBG\_INVOKE\_编辑器环境变量确定打开的编辑器。 例如，考虑以下值的 WINDBG\_INVOKE\_编辑器。

```reg
c:\my\path\myeditor.exe -file %f -line %l
```

此值指示 Myeditor.exe 将打开到当前源文件的基于 1 的行号。 **%L**选项指示该行应为一个基于，读取数字并 **%f**指示应使用当前的源文件。 此外可以包括 **%L**指示的行号是从零开始或 **%p**若要指示应使用当前的源文件。

 

 





