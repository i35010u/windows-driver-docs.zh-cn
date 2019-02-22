---
title: bs （更新断点命令）
description: Bs 命令更改时遇到指定的断点执行的命令。
ms.assetid: 624c9a30-a0d8-49bd-aba6-a46250022677
keywords:
- bs （更新断点命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bs (Update Breakpoint Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 093a1550ed7c30ead4f7714ccef515dd38c06a90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555002"
---
# <a name="bs-update-breakpoint-command"></a>bs （更新断点命令）


**Bs**命令更改时遇到指定的断点执行的命令。

```dbgcmd
bs ID ["CommandString"] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
指定断点的 ID 号。

<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定要执行每次遇到该断点的命令的新列表。 必须将*CommandString*在引号中的参数。 使用分号分隔多个命令。

调试器中的命令*CommandString*可以包括参数。 可以使用标准的 C-控制字符 (如 **\\n**并 **\\"**)。 包含在第二级别引号中的分号 (**\\"**) 被解释为属于嵌入带引号的字符串。

*CommandString*仅当到达断点时，应用程序执行响应时执行命令**g （转向）** 命令。 如果您要单步执行代码或跟踪忽略这一点，不会执行命令。

任一命令恢复程序执行在断点后的 (如**g**或**t**) 结束执行命令列表。

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

 

 





