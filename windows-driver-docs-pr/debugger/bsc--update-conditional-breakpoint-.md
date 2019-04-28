---
title: bsc（更新条件断点）
description: Bsc 命令更改的条件在其下一个断点发生或发生更改时遇到指定条件断点执行的命令。
ms.assetid: 4d491797-3ba2-4a63-a575-67df39484bcf
keywords:
- bsc （更新条件断点） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bsc (Update Conditional Breakpoint)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a0fc70c55d4dbeb8e6e00e5836c80e1d98f6262
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347825"
---
# <a name="bsc-update-conditional-breakpoint"></a>bsc（更新条件断点）


**Bsc**命令更改的条件在其下一个断点发生或发生更改时遇到指定条件断点执行的命令。

```dbgcmd
bsc ID Condition ["CommandString"] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定断点的 ID 号。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *Condition*   
指定应在其下触发断点的条件。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定要执行每次遇到该断点的命令的新列表。 必须将*CommandString*在引号中的参数。 使用分号分隔多个命令。

调试器中的命令*CommandString*可以包括参数。 可以使用标准的 C-控制字符 (如 **\\n**并 **\\"**)。 包含在第二级别引号中的分号 (**\\"**) 被解释为属于嵌入带引号的字符串。

仅当到达断点时，应用程序执行响应时，会执行 CommandString 命令**g （转向）** 命令。 如果您要单步执行代码或跟踪忽略这一点，不会执行命令。

任一命令恢复程序执行在断点后的 (如**g**或**t**) 结束执行命令列表。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>M节点</p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和如何使用断点、 其他断点的命令和控制断点的方法以及如何从内核调试程序在用户空间中设置断点的示例，请参阅[使用断点](using-breakpoints.md)。 有关条件断点的详细信息，请参阅[设置条件断点](setting-a-conditional-breakpoint.md)。

<a name="remarks"></a>备注
-------

如果*CommandString*未指定，则会删除任何已设置断点的命令。

可以通过使用实现相同的效果[ **bs （更新断点命令）** ](bs--update-breakpoint-command-.md)命令使用以下语法：

```dbgcmd
bs ID "j Condition 'CommandString'; 'gc'"
```

 

 





