---
title: ~（线程状态）
description: 颚化 (~) 命令显示指定线程或当前进程中的所有线程的状态。
keywords:
- ~ (线程状态) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ~ (Thread Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f44138693507365f843b229357f6991f04c90ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800185"
---
# <a name="-thread-status"></a>~（线程状态）


"颚化符 (**~**) " 命令显示指定线程或当前进程中的所有线程的状态。

```dbgcmd
~ Thread
```

## <a name="span-idddk_cmd_thread_status_dbgspanspan-idddk_cmd_thread_status_dbgspanparameters"></a><span id="ddk_cmd_thread_status_dbg"></span><span id="DDK_CMD_THREAD_STATUS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要显示的线程。 如果省略此参数，则显示所有线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

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

只能在用户模式下指定线程。 在内核模式下，波形符 (**~**) 是指处理器。

你可以在多个命令之前添加线程符号。 若要详细了解波形符 (**~**) 后跟一个命令的含义，请参阅命令本身的条目。

下面的示例演示如何使用此命令。 以下命令显示所有线程。

```dbgcmd
0:001> ~
```

以下命令还显示所有线程。

```dbgcmd
0:001> ~*
```

以下命令显示当前处于活动状态的线程。

```dbgcmd
0:001> ~.
```

以下命令显示最初导致异常 (或在调试器附加到进程) 时处于活动状态的线程。

```dbgcmd
0:001> ~#
```

以下命令显示第2线程。

```dbgcmd
0:001> ~2
```

前面的命令显示以下输出。

```dbgcmd
0:001> ~
   0 id: 4dc.470 Suspend: 0 Teb 7ffde000 Unfrozen
. 1 id: 4dc.534 Suspend: 0 Teb 7ffdd000 Unfrozen
#  2 id: 4dc.5a8 Suspend: 0 Teb 7ffdc000 Unfrozen
```

在此输出的第一行，0是小数线程号，4DC 是十六进制的进程 ID，470是十六进制线程 ID，0x7FFDE000 是 TEB 的地址，而 **解冻** 的是线程状态。 在线程1之前 )  (，这意味着此线程为当前线程。 线程2前面的数字符号 (\#) 意味着此线程最初引发异常，或者在调试器附加到进程时它处于活动状态。

 

 





