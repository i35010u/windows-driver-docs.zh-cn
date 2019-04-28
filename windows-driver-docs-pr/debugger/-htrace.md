---
title: htrace
description: Htrace 扩展显示堆栈跟踪信息的一个或多个句柄。
ms.assetid: 1da92c8d-8f77-4b30-a908-bcc33ad05cce
keywords:
- 句柄，htrace 扩展
- htrace Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- htrace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e74f5d92ba334153c61b8c92c0d49c7619d71287
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336476"
---
# <a name="htrace"></a>!htrace


**！ Htrace**扩展显示堆栈跟踪信息的一个或多个句柄。

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

## <a name="span-idddkhtracedbgspanspan-idddkhtracedbgspanparameters"></a><span id="ddk__htrace_dbg"></span><span id="DDK__HTRACE_DBG"></span>参数


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *句柄*   
指定将显示其堆栈跟踪的句柄。 如果*处理*为 0 或省略，就会显示在过程中的所有句柄的堆栈跟踪。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
（仅适用于内核模式）指定将显示其句柄的进程。 如果*进程*为 0 或省略，则当前进程使用。 在用户模式下，始终使用当前进程。

<span id="_______Max_Traces______"></span><span id="_______max_traces______"></span><span id="_______MAX_TRACES______"></span> *最大\_跟踪*   
指定要显示的堆栈跟踪的最大数目。 在用户模式下，如果省略此参数，然后在目标进程的所有堆栈跟踪将都显示。

<span id="_______-enable______"></span><span id="_______-ENABLE______"></span> **-enable**   
（仅限用户模式）启用句柄跟踪，并获取要用作由的初始状态的句柄信息的第一个快照 **-差异**选项。

<span id="_______-snapshot______"></span><span id="_______-SNAPSHOT______"></span> **-snapshot**   
（仅限用户模式）获取当前的句柄信息，以用作由的初始状态的快照 **-差异**选项。

<span id="_______-diff______"></span><span id="_______-DIFF______"></span> **-diff**   
（仅限用户模式）将当前与上一个快照的拍摄的句柄信息的句柄信息进行比较。 显示所有仍是打开的句柄。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span> **-disable**   
（用户模式下仅;Windows Server 2003 及更高版本) 禁用处理跟踪。 在 Windows XP 中，可以仅通过终止目标进程禁用句柄跟踪。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p></p>
Kdexts.dll Ntsdexts.dll</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关控点的信息，请参阅 Microsoft Windows SDK 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）若要进一步显示有关特定句柄的信息，请使用[ **！ 处理**](-handle.md)扩展。

<a name="remarks"></a>备注
-------

之前 **！ htrace**可以使用，处理必须启用跟踪。 若要启用句柄跟踪的一种方法是输入 **！ htrace-启用**命令。 启用句柄跟踪，堆栈跟踪信息保存每个时间对进程打开了句柄，关闭了句柄，或引用无效的句柄。 它是此堆栈跟踪信息的 **！ htrace**显示。

**请注意**  还可以启用通过目标进程的激活应用程序验证器并选择跟踪句柄**处理**选项。

 

某些跟踪报告 **！ htrace**可能来自不同的进程上下文。 在这种情况下，返回地址在当前进程上下文中，可能无法正确解析，或者可能会解析为错误的符号。

下面的示例显示进程 0x81400300 中有关所有句柄的信息：

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

 

 





