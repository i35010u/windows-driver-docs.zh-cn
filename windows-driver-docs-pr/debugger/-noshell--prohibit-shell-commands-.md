---
title: .noshell（禁止 Shell 命令）
description: Noshell 命令阻止你使用 shell 命令。
keywords:
- noshell (禁止 Shell 命令) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .noshell (Prohibit Shell Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 199cd8de0e25edb9bc367d1fb942d1e4334ab674
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803307"
---
# <a name="noshell-prohibit-shell-commands"></a>.noshell（禁止 Shell 命令）


**Noshell** 命令阻止你使用 [**shell**](-shell--command-shell-.md)命令。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关命令行界面和禁用 shell 命令的其他方法的详细信息，请参阅 [使用 Shell 命令](using-shell-commands.md)。

<a name="remarks"></a>备注
-------

如果使用 **noshell** 命令，则只要调试器正在运行，就不能使用 [**命令行界面 (命令行界面)**](-shell--command-shell-.md) 命令。

如果要执行远程调试，此命令可用于安全目的。

 

 





