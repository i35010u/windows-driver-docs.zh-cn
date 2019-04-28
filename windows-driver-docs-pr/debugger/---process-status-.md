---
title: （进程状态）
description: 管道 （） 命令显示指定进程或当前正在调试的所有进程的状态。不要混淆此命令使用 （系统状态） 命令。
ms.assetid: 78f53049-e949-4431-b6b1-0710da047ced
keywords:
- （进程状态）Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Process Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3af3ba4af34516df61e3826e759be964c495f3e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334846"
---
# <a name="-process-status"></a>|（进程状态）


管道 (**|**) 命令显示指定进程的状态或当前正在调试你的所有进程。

不要将使用此命令相混淆[ **| |（系统状态）** ](----system-status-.md)命令。

```dbgcmd
    | Process
```

## <a name="span-idddkcmdprocessstatusdbgspanspan-idddkcmdprocessstatusdbgspanparameters"></a><span id="ddk_cmd_process_status_dbg"></span><span id="DDK_CMD_PROCESS_STATUS_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
指定要显示的进程。 如果省略此参数，将显示所有正在调试的进程。 有关语法的详细信息，请参阅[过程语法](process-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
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

有关详细信息和显示或控制进程和线程的其他方法，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

仅在用户模式下，可以指定进程。

您可以添加很多命令之前的过程符号。 有关管道的含义的详细信息 (**|**) 后接一个命令，请参阅命令本身的条目。

除非您启用了调试子进程，在启动调试会话时，没有可供调试器的仅有一个进程。

下面的示例显示如何使用此命令。 下面的命令显示所有进程。

```dbgcmd
2:005> |
```

以下命令还显示所有进程。

```dbgcmd
2:005> |*
```

下面的命令显示当前活动的进程。

```dbgcmd
2:005> |.
```

下面的命令显示的进程的最初引发异常 （或到最初附加调试器）。

```dbgcmd
2:005> |#
```

下面的命令显示进程号 2。

```dbgcmd
2:005> |2
```

前一个命令显示以下输出。

```dbgcmd
0:002> |
#  0 id: 224   name: myprog.exe 
   1 id: 228   name: onechild.exe 
. 2 id: 22c   name: anotherchild.exe 
```

此输出在第一行，0 是十进制进程号、 224 是十六进制的进程 ID，并*Myprog.exe*是进程的应用程序名称。 句点 （.） 之前进程 2 意味着，此过程是当前进程。 数字符号 (\#) 进程 0 意味着此进程是最初引发异常的一个或调试器附加到之前。

 

 





