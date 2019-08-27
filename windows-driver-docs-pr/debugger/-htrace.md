---
title: htrace
description: Htrace 扩展显示一个或多个句柄的堆栈跟踪信息。
ms.assetid: 1da92c8d-8f77-4b30-a908-bcc33ad05cce
keywords:
- 句柄, htrace 扩展
- htrace Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- htrace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4245fa9056c587f1592d52e4e678c2f15a8145f6
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025236"
---
# <a name="htrace"></a>!htrace


**! Htrace** extension 显示一个或多个句柄的堆栈跟踪信息。

用户模式语法

```dbgcmd
!htrace [Handle [Max_Traces]] 
!htrace -enable [Max_Traces]
!htrace -snapshot
!htrace -diff
!htrace -disable
!htrace -? 
```

内核模式语法

```dbgcmd
    !htrace [Handle [Process [Max_Traces]]] 
!htrace -? 
```

## <a name="span-idddk__htrace_dbgspanspan-idddk__htrace_dbgspanparameters"></a><span id="ddk__htrace_dbg"></span><span id="DDK__HTRACE_DBG"></span>Parameters


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
指定将显示其堆栈跟踪的句柄。 如果*Handle*为0或省略, 则将显示进程中所有句柄的堆栈跟踪。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
(仅限内核模式)指定将显示其句柄的进程。 如果*Process*为0或省略, 则使用当前进程。 在用户模式下, 始终使用当前进程。

<span id="_______Max_Traces______"></span><span id="_______max_traces______"></span><span id="_______MAX_TRACES______"></span>*最\_大跟踪*   
指定要显示的堆栈跟踪的最大数目。 在用户模式下, 如果省略此参数, 则将显示目标进程的所有堆栈跟踪。

<span id="_______-enable______"></span><span id="_______-ENABLE______"></span> **-enable**   
(仅用户模式)启用句柄跟踪, 并获取句柄信息的第一个快照, 以用作**差异**选项的初始状态。

<span id="_______-snapshot______"></span><span id="_______-SNAPSHOT______"></span> **-snapshot**   
(仅用户模式)拍摄当前句柄信息的快照, 以用作 **-diff**选项的初始状态。

<span id="_______-diff______"></span><span id="_______-DIFF______"></span> **-差异**   
(仅用户模式)将当前句柄信息与所采用的句柄信息的最后一个快照进行比较。 显示所有仍处于打开状态的句柄。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span> **-disable**   
(仅用户模式;仅限 Windows Server 2003 及更高版本) 禁用处理跟踪。 在 Windows XP 中, 只能通过终止目标进程来禁用句柄跟踪。

<span id="_______-_______"></span> **-?**    
在调试器命令窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p></p>
Kdexts Ntsdexts</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关句柄的信息, Microsoft Windows SDK 请参阅 Russinovich 文档和*Microsoft Windows 内部机制*, 并标记和 David 所罗门群岛。 若要显示有关特定句柄的详细信息, 请使用[ **! 句柄**](-handle.md)扩展。

<a name="remarks"></a>备注
-------

之前, 必须启用句柄跟踪, 然后才能使用**htrace** 。 启用句柄跟踪的一种方法是输入 **! htrace**命令。 启用了句柄跟踪后, 每次进程打开句柄、关闭句柄或引用无效句柄时, 都会保存堆栈跟踪信息。 这是 **! htrace**显示的此堆栈跟踪信息。

**请注意**   , 您还可以通过激活目标进程的应用程序验证工具, 然后选择 "**句柄**" 选项来启用处理跟踪。

 

由 **! htrace**报告的某些跟踪可能来自不同的进程上下文。 在这种情况下, 返回地址在当前进程上下文中可能无法正确解析, 或可能解析为错误的符号。

下面的示例显示有关进程0x81400300 中的所有句柄的信息:

```dbgcmd
kd> !htrace 0 81400300
Process 0x81400300
ObjectTable 0xE10CCF60
## 

Handle 0x7CC - CLOSE:
0x8018FCB9: ntoskrnl!ExDestroyHandle+0x103
0x801E1D12: ntoskrnl!ObpCloseHandleTableEntry+0xE4
0x801E1DD9: ntoskrnl!ObpCloseHandle+0x85
0x801E1EDD: ntoskrnl!NtClose+0x19
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7CC - OPEN:
0x8018F44A: ntoskrnl!ExCreateHandle+0x94
0x801E3390: ntoskrnl!ObpCreateUnnamedHandle+0x10C
0x801E7317: ntoskrnl!ObInsertObject+0xC3
0x77DE23B2: KERNEL32!CreateSemaphoreA+0x66
0x010011C5: badhandle!main+0x45
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7DC - BAD REFERENCE:
0x8018F709: ntoskrnl!ExMapHandleToPointerEx+0xEA
0x801E10F2: ntoskrnl!ObReferenceObjectByHandle+0x12C
0x801902BE: ntoskrnl!NtSetEvent+0x6C
0x80154965: ntoskrnl!_KiSystemService+0xC4
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7DC - CLOSE:
0x8018FCB9: ntoskrnl!ExDestroyHandle+0x103
0x801E1D12: ntoskrnl!ObpCloseHandleTableEntry+0xE4
0x801E1DD9: ntoskrnl!ObpCloseHandle+0x85
0x801E1EDD: ntoskrnl!NtClose+0x19
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7DC - OPEN:
0x8018F44A: ntoskrnl!ExCreateHandle+0x94
0x801E3390: ntoskrnl!ObpCreateUnnamedHandle+0x10C
0x801E7317: ntoskrnl!ObInsertObject+0xC3
0x77DE265C: KERNEL32!CreateEventA+0x66
0x010011A0: badhandle!main+0x20
0x010012C1: badhandle!mainCRTStartup+0xE3
0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D
## 

Parsed 0x6 stack traces.
Dumped 0x5 stack traces.
```

 

 





