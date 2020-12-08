---
title: .idle_cmd（设置空闲命令）
description: .Idle_cmd 命令设置空闲命令。 这是每当控件从目标返回到调试器时执行的命令。
keywords:
- 在 Windows 调试) .idle_cmd (设置空闲命令
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .idle_cmd (Set Idle Command)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4191b93f61bc1fd74d67bd7ac5267252fa99f9b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817033"
---
# <a name="idle_cmd-set-idle-command"></a>。空闲 \_ cmd (设置空闲命令) 


**Idle \_ cmd** 命令设置 *空闲命令*。 这是每当控件从目标返回到调试器时执行的命令。 例如，当目标到达断点时，将执行此命令。

```dbgcmd
.idle_cmd
.idle_cmd String 
.idle_cmd /d
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______String______"></span><span id="_______string______"></span><span id="_______STRING______"></span>*字符串*   
指定应将空闲命令设置为的字符串。

<span id="________d______"></span><span id="________D______"></span>**/d**   
清除 "空闲" 命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

无法在脚本文件中使用此命令。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当为时，不使用参数时 **，将显示 \_** 当前空闲命令。

在 WinDbg 中，空闲命令存储在工作区中。

示例如下。 Idle 命令设置为 [**r eax**](r--registers-.md)。 然后，由于调试器已经处于空闲状态，因此此命令会立即执行，并显示 **eax** 注册：

```dbgcmd
windbg> .idle_cmd r eax 
Execute when idle: r eax
eax=003b0de8
```

 

 





