---
title: ~ （线程状态）
description: 波形符 （~） 命令显示当前进程中指定的线程或所有线程的状态。
ms.assetid: c27e4c72-86da-459d-833f-d27d26bdea0e
keywords:
- ~ （线程状态） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ~ (Thread Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42c87cbfb06cd0afb50b2f1da6275ecfea8dfe77
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524920"
---
# <a name="-thread-status"></a>~ （线程状态）


波形符 (**~**) 命令显示当前进程中的指定线程或所有线程的状态。

```dbgcmd
~ Thread
```

## <a name="span-idddkcmdthreadstatusdbgspanspan-idddkcmdthreadstatusdbgspanparameters"></a><span id="ddk_cmd_thread_status_dbg"></span><span id="DDK_CMD_THREAD_STATUS_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定要显示的线程。 如果省略此参数，将显示所有线程。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

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

仅在用户模式下，可以指定线程。 在内核模式下，波形符 (**~**) 指的是一个处理器。

您可以添加很多命令之前的线程符号。 有关详细信息的含义的波形符 (**~**) 后面输入命令，请参阅命令本身的条目。

下面的示例显示如何使用此命令。 下面的命令显示所有线程。

```dbgcmd
0:001> ~
```

以下命令还显示所有线程。

```dbgcmd
0:001> ~*
```

下面的命令显示当前处于活动状态的线程。

```dbgcmd
0:001> ~.
```

下面的命令显示的线程的最初引发异常 （或，调试器附加到进程时处于活动状态）。

```dbgcmd
0:001> ~#
```

下面的命令显示线程号 2。

```dbgcmd
0:001> ~2
```

前一个命令显示以下输出。

```dbgcmd
0:001> ~
   0 id: 4dc.470 Suspend: 0 Teb 7ffde000 Unfrozen
. 1 id: 4dc.534 Suspend: 0 Teb 7ffdd000 Unfrozen
#  2 id: 4dc.5a8 Suspend: 0 Teb 7ffdc000 Unfrozen
```

此输出在第一行，0 是十进制线程号、 4DC 是十六进制的进程 ID、 470 是十六进制的线程 ID、 0x7FFDE000 是 TEB 的地址和**Unfrozen**是线程的状态。 线程 1 之前将句点 （.） 表示此线程是当前线程。 数字符号 (\#) 线程 2 意味着此线程是最初引发异常的一个或处于活动状态之前当调试器附加到进程。

 

 





