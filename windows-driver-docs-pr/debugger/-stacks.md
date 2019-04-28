---
title: 堆栈
description: 堆栈扩展显示有关内核堆栈的信息。
ms.assetid: f0777609-4785-4a6b-a6f5-9efaeb608df7
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
ms.openlocfilehash: 3fb605c7615cbec848300063f41a9281f4b26d20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334236"
---
# <a name="stacks"></a>!stacks


**！ 堆栈**扩展显示有关内核堆栈的信息。

语法

```dbgcmd
!stacks [Detail [FilterString]] 
```

## <a name="span-idddkstacksdbgspanspan-idddkstacksdbgspanparameters"></a><span id="ddk__stacks_dbg"></span><span id="DDK__STACKS_DBG"></span>参数


<span id="_______Detail______"></span><span id="_______detail______"></span><span id="_______DETAIL______"></span> *详细信息*   
指定要在显示中使用详细信息的级别。 下表列出了有效值*详细信息*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>显示当前的内核堆栈的摘要。 这是默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>显示当前分页，堆栈，以及当前的内核堆栈。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>显示所有堆栈，以及当前调出的堆栈和当前的内核堆栈的完整参数。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______FilterString______"></span><span id="_______filterstring______"></span><span id="_______FILTERSTRING______"></span> *FilterString*   
显示包含符号中指定的子字符串的线程。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关内核堆栈的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

**！ 堆栈**扩展为提供的每个线程的状态的简短摘要。 您可以使用此扩展而不是[ **！ 过程**](-process.md)扩展以获取系统的快速概述，尤其是在调试多线程问题，例如资源冲突或死锁。

[ **！ Findstack** ](-findstack.md)用户模式下扩展还会显示有关特定堆栈的信息。

下面是简单的示例 **！ 堆栈**显示：

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

第一列显示进程 ID 和线程 ID （由句点分隔）。

第二列是当前线程的 ETHREAD 块的地址。

第三列显示线程 （初始化，准备就绪、 正在运行、 备用、 已终止，转换，或阻止） 的状态。

第四列显示线程的堆栈上的顶部的地址。

下面是示例的更多详细 **！ 堆栈**输出：

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

 

 





