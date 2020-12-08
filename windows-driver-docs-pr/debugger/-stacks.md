---
title: 排列
description: 堆栈扩展显示有关内核堆栈的信息。
keywords:
- 堆栈 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- stacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 01dcfe17909776a84b38af39be8466cf80cbffb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826201"
---
# <a name="stacks"></a>!stacks


**！** Stack 扩展显示有关内核堆栈的信息。

语法

```dbgcmd
!stacks [Detail [FilterString]] 
```

## <a name="span-idddk__stacks_dbgspanspan-idddk__stacks_dbgspanparameters"></a><span id="ddk__stacks_dbg"></span><span id="DDK__STACKS_DBG"></span>参数


<span id="_______Detail______"></span><span id="_______detail______"></span><span id="_______DETAIL______"></span>*详细信息*   
指定要在显示中使用的详细信息的级别。 下表列出了 *详细信息* 的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>显示当前内核堆栈的摘要。 这是默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>显示当前分页的堆栈以及当前内核堆栈。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>显示所有堆栈的完整参数，以及当前已分页和当前内核堆栈的堆栈。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______FilterString______"></span><span id="_______filterstring______"></span><span id="_______FILTERSTRING______"></span>*FilterString*   
仅显示符号中包含指定子字符串的线程。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内核堆栈的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。 

<a name="remarks"></a>备注
-------

**！** Stack 扩展提供每个线程的状态的简短摘要。 您可以使用此扩展而不是 [**！进程**](-process.md) 扩展来快速了解系统，尤其是在调试资源冲突或死锁等多线程问题时。

[**！ Findstack**](-findstack.md)用户模式扩展还显示有关特定堆栈的信息。

下面是最简单的 **！** stack 显示示例：

```dbgcmd
kd> !stacks 0
Proc.Thread  .Thread  ThreadState  Blocker
                                     [System]
   4.000050  827eea10  Blocked    +0xfe0343a5

                                     [smss.exe]

                                     [csrss.exe]
  b0.0000a8  82723b70  Blocked    ntoskrnl!_KiSystemService+0xc4
  b0.0000c8  82719620  Blocked    ntoskrnl!_KiSystemService+0xc4
  b0.0000d0  827d5d50  Blocked    ntoskrnl!_KiSystemService+0xc4
.....
```

第一列显示进程 ID 和线程 ID (用句点分隔) 。

第二列是线程的 ETHREAD 块的当前地址。

第三列显示线程的状态 (初始化、就绪、正在运行、备用、终止、转换或阻塞) 。

第四列显示线程堆栈上的顶层地址。

下面是更详细 **！堆栈** 输出的示例：

```dbgcmd
kd> !stacks 1
Proc.Thread  .Thread  ThreadState  Blocker
                                     [System]
   4.000008  827d0030  Blocked    ntoskrnl!MmZeroPageThread+0x66
   4.000010  827d0430  Blocked    ntoskrnl!ExpWorkerThread+0x189
   4.000014  827cf030  Blocked    Stack paged out
   4.000018  827cfda0  Blocked    Stack paged out
   4.00001c  827cfb10  Blocked    ntoskrnl!ExpWorkerThread+0x189
.....
                                     [smss.exe]
  9c.000098  82738310  Blocked    Stack paged out
  9c.0000a0  826a5190  Blocked    Stack paged out
  9c.0000a4  82739d30  Blocked    Stack paged out

                                     [csrss.exe]
  b0.0000bc  826d0030  Blocked    Stack paged out
  b0.0000b4  826c9030  Blocked    Stack paged out
  b0.0000a8  82723b70  Blocked    ntoskrnl!_KiSystemService+0xc4
.....

kd> !stacks 2
Proc.Thread  .Thread  ThreadState  Blocker
                                     [System]
   4.000008  827d0030  Blocked    ntoskrnl!KiSwapThread+0xc5
                                  ntoskrnl!KeWaitForMultipleObjects+0x2b4
                                  ntoskrnl!MmZeroPageThread+0x66
                                  ntoskrnl!Phase1Initialization+0xd82
                                  ntoskrnl!PspSystemThreadStartup+0x4d
                                  ntoskrnl!CreateSystemRootLink+0x3d8
                                  +0x3f3f3f3f
   4.000010  827d0430  Blocked    ntoskrnl!KiSwapThread+0xc5
                                  ntoskrnl!KeRemoveQueue+0x191
.....
```

 

 





