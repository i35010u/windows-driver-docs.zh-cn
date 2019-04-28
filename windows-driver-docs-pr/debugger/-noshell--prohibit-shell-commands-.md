---
title: .noshell（禁止 Shell 命令）
description: .Noshell 命令防止使用.shell 命令。
ms.assetid: 49a83e46-1390-4b60-bd61-a5da80c513e3
keywords:
- .noshell （禁止 Shell 命令） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .noshell (Prohibit Shell Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f51d8dd0333b8630456aa45fc3cb2e2bf05cc75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335896"
---
# <a name="noshell-prohibit-shell-commands"></a>.noshell（禁止 Shell 命令）


**.Noshell**命令将使您无法使用[ **.shell** ](-shell--command-shell-.md)命令。

```dbgcmd
.noshell 
```

## <span id="ddk_meta_prohibit_shell_commands_dbg"></span><span id="DDK_META_PROHIBIT_SHELL_COMMANDS_DBG"></span>


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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关命令行界面的详细信息并禁用 shell 命令的其他方法，请参阅[使用 Shell 命令](using-shell-commands.md)。

<a name="remarks"></a>备注
-------

如果您使用 **.noshell**命令时，不能使用[ **.shell （命令行界面）** ](-shell--command-shell-.md)命令，只要运行调试器，即使在开始新的调试会话。

如果您在执行远程调试，此命令可用于安全目的。

 

 





