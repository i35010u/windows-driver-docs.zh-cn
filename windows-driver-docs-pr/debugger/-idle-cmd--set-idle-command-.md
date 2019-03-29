---
title: .idle_cmd（设置空闲命令）
description: .Idle_cmd 命令设置的空闲状态的命令。 这是控制将返回从目标到调试器时执行的命令。
ms.assetid: 8cfe7aa8-4e31-4e97-b61d-9e8bb1b7be61
keywords:
- .idle_cmd （set 空闲命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .idle_cmd (Set Idle Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 551d784cf4e1ed7c18aa6cb9ef36bcdd7937743b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575394"
---
# <a name="idlecmd-set-idle-command"></a>.idle\_cmd （设置空闲命令）


**.Idle\_cmd**命令集*空闲命令*。 这是控制将返回从目标到调试器时执行的命令。 例如，当目标到达断点时，此命令执行。

```dbgcmd
.idle_cmd
.idle_cmd String 
.idle_cmd /d
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span> *字符串*   
指定应设置为空闲状态的命令的字符串。

<span id="________d______"></span><span id="________D______"></span> **/d**   
清除空闲命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

不能在脚本文件中使用此命令。

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

当 **.idle\_cmd**使用不带任何参数，它显示当前空闲命令。

在 WinDbg 中，空闲命令存储在工作区中。

下面是一个示例。 空闲命令设置为[ **r eax**](r--registers-.md)。 然后，在调试器已处于空闲状态，因为此命令立即执行，显示**eax**注册：

```dbgcmd
windbg> .idle_cmd r eax 
Execute when idle: r eax
eax=003b0de8
```

 

 





