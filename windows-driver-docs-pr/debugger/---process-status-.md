---
title: " (进程状态) "
description: 管道 ( ) 命令显示指定进程的状态，或显示当前正在调试的所有进程的状态。请勿将此命令与 (系统状态) 命令混淆。
keywords:
- ) Windows 调试 (处理状态
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Process Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7b97118f61c035f1c80010c6713d7e853635f14e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800195"
---
# <a name="-process-status"></a>|（进程状态）


管道 (**|**) 命令显示指定进程的状态，或显示当前正在调试的所有进程的状态。

不要将此命令与 [**| | (系统状态)**](----system-status-.md) 命令混淆。

```dbgcmd
    | Process
```

## <a name="span-idddk_cmd_process_status_dbgspanspan-idddk_cmd_process_status_dbgspanparameters"></a><span id="ddk_cmd_process_status_dbg"></span><span id="DDK_CMD_PROCESS_STATUS_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
指定要显示的进程。 如果省略此参数，则将显示正在调试的所有进程。 有关语法的详细信息，请参阅 [处理语法](process-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
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

有关显示或控制进程和线程的其他方法的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

只能在用户模式下指定进程。

你可以在多个命令前添加一个进程符号。 有关管道 (**|**) 后跟一个命令的含义的详细信息，请参阅命令本身的条目。

在启动调试会话时，除非已启用子进程调试，否则调试器只有一个可用的进程。

下面的示例演示如何使用此命令。 以下命令显示所有进程。

```dbgcmd
2:005> |
```

以下命令还显示所有进程。

```dbgcmd
2:005> |*
```

以下命令显示当前处于活动状态的进程。

```dbgcmd
2:005> |.
```

以下命令显示最初导致异常 (或调试器最初附加到) 的进程。

```dbgcmd
2:005> |#
```

以下命令显示进程编号2。

```dbgcmd
2:005> |2
```

前面的命令显示以下输出。

```dbgcmd
0:002> |
#  0 id: 224   name: myprog.exe 
   1 id: 228   name: onechild.exe 
. 2 id: 22c   name: anotherchild.exe 
```

在此输出的第一行，0是小数进程号，224是十六进制进程 ID， *Myprog.exe* 是进程的应用程序名称。 句点 ( 在进程2之前 ) 表示此进程是当前进程。 # Sign (\# 在进程0之前) 表示此进程是最初导致异常的进程，或者是附加到调试器的进程。

 

 





