---
title: .jdinfo（使用 JIT_DEBUG_INFO）
description: .Jdinfo 命令使用 JIT_DEBUG_INFO 结构作为上下文只需在实时 (JIT) 调试异常的源。
ms.assetid: C35A2A04-CF0E-475e-8471-2A8562BB3650
keywords:
- 使用 JIT_DEBUG_INFO (.jdinfo) 命令---附录
- JIT_DEBUG_INFO ----- Appendix
- .jdinfo （使用 JIT_DEBUG_INFO） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .jdinfo (Use JIT_DEBUG_INFO)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42874c723d864c0596ac225a4166d4ac220f0eb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336344"
---
# <a name="jdinfo-use-jitdebuginfo"></a>.jdinfo (使用 JIT\_调试\_信息)


**.Jdinfo**命令使用 JIT\_调试\_作为上下文只需在实时 (JIT) 调试异常的源信息结构。 向结构的地址传递给 **.jdinfo**命令使用 AeDebug 注册表项中指定的 %p 参数。

有关使用的注册表项的详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。 有关注册上下文的详细信息，请参阅[更改上下文](changing-contexts.md)。

```dbgcmd
.jdinfo Address 
```

## <a name="span-idddkapcmetausejitdebuginfodbgspanspan-idddkapcmetausejitdebuginfodbgspanparameters"></a><span id="ddk_apc_meta_use_jit_debug_info_dbg"></span><span id="DDK_APC_META_USE_JIT_DEBUG_INFO_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址的 JIT\_调试\_信息结构。 向结构的地址传递给 **.jdinfo**命令使用 AeDebug 注册表项中指定的 %p 参数。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式</p></td>
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

 

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例

此示例演示如何配置 AeDebug 注册表项以使用 WinDbg 可以用作 JIT 调试器。

```dbgcmd
Debugger = "Path\WinDbg.EXE -p %ld -e %ld -c ".jdinfo 0x%p"
```

然后，当发生故障时，调用配置的 JIT 调试器并 %p 参数用于传递 JIT 的地址\_调试\_信息结构 **.jdinfo**后调试器执行的命令已启动。

```dbgcmd
nMicrosoft (R) Windows Debugger Version 10.0.10240.9 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

*** wait with pending attach
Executable search path is: 
...
ModLoad: 00000000`68a20000 00000000`68ac3000   C:\WINDOWS\WinSxS\amd64_microsoft.vc90.crt_1fc8b3b9a1e18e3b_9.0.30729.9247_none_08e394a1a83e212f\MSVCR90.dll
(153c.5d0): Break instruction exception - code 80000003 (first chance)
Processing initial command '.jdinfo 0x00000000003E0000'
ntdll!DbgBreakPoint:
00007ffc`81a986a0 cc              int     3
0:003> .jdinfo 0x00000000003E0000
----- Exception occurred on thread 0:15c8
ntdll!ZwWaitForMultipleObjects+0x14:
00007ffc`81a959a4 c3              ret

----- Exception record at 00000000`003e0028:
ExceptionAddress: 00007ff791d81014 (CrashAV_x64!wmain+0x0000000000000014)
   ExceptionCode: c0000005 (Access violation)
  ExceptionFlags: 00000000
NumberParameters: 2
   Parameter[0]: 0000000000000001
   Parameter[1]: 0000000000000000
Attempt to write to address 0000000000000000

----- Context record at 00000000`003e00c0:
rax=0000000000000000 rbx=0000000000000000 rcx=00007ffc81a954d4
rdx=0000000000000000 rsi=0000000000000000 rdi=0000000000000001
rip=00007ff791d81014 rsp=00000000006ff8b0 rbp=0000000000000000
 r8=00000000006ff808  r9=0000000000000000 r10=0000000000000000
r11=0000000000000000 r12=0000000000000000 r13=0000000000000000
r14=0000000000000000 r15=0000000000000000
iopl=0         nv up ei pl zr na po nc
cs=0033  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00010246
CrashAV_x64!wmain+0x14:
00007ff7`91d81014 45891b          mov     dword ptr [r11],r11d ds:00000000`00000000=????????
```

<a name="remarks"></a>备注
-------

**.Jdinfo**命令使用**AeDebug**在 Windows Vista 中引入的注册表信息。 有关使用的注册表项的详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。 **.Jdinfo**命令将 JIT 的地址\_调试\_信息的系统设置了**AeDebug**并将上下文设置到导致崩溃的原因的异常。

可以使用 **.jdinfo**命令而不是 **-g**中**AeDebug**具有您的调试器设置为**AeDebug**状态而无需执行。

此状态可以是有利的因为通常情况下，用户模式异常发生时，发生以下序列：

1.  Microsoft Windows 操作系统将暂停执行应用程序。

2.  启动事后调试器。

3.  将调试器附加到应用程序。

4.  调试器将会发出"Go"命令。 (此命令引起 **-g**中**AeDebug**键。)

5.  目标会尝试执行并可能会或可能不会遇到相同的异常。

6.  此异常中断到调试器。

有可能发生这些事件发生的几个问题：

-   异常不始终会重复，可能是由于临时性条件不再存在时重新启动该异常。

-   另一个事件，如其他异常，可能会出现。 没有无法知道它是否与相同原始事件。

-   将调试器附加涉及到插入一个新线程，如果一个线程持有加载程序锁可以阻止。 插入新线程可以是过程的重要错误和干扰。

如果您使用 **-c.jdinfo**而不是 **-g**在你**AeDebug**密钥，不会执行。 相反，异常信息检索从 JIT\_调试\_使用 %p 变量的信息结构。

例如，请考虑以下**AeDebug**密钥。

```dbgcmd
ntsd -p %ld -e %ld -c ".jdinfo 0x%p"
```

下面的示例是较低的侵入性。 **-Pv**开关将使调试器附加 noninvasively，这不会插入到目标中，任何新线程。

```dbgcmd
ntsd -pv -p %ld -e %ld -c ".jdinfo 0x%p"
```

如果使用此非侵入的选项，退出调试器不会结束该过程。 可以使用[ **.kill （终止进程）** ](-kill--kill-process-.md)命令以结束进程。

如果你想要用于此转储文件调试，则应使用[ **.dump /j** ](-dump--create-dump-file-.md)若要添加 JIT\_调试\_转储文件，创建转储文件时的信息结构。

JIT\_调试\_信息结构定义，如下所示。

```dbgcmd
typedef struct _JIT_DEBUG_INFO {
    DWORD dwSize;
    DWORD dwProcessorArchitecture;
    DWORD dwThreadID;
    DWORD dwReserved0;
    ULONG64 lpExceptionAddress;
    ULONG64 lpExceptionRecord;
    ULONG64 lpContextRecord;
} JIT_DEBUG_INFO, *LPJIT_DEBUG_INFO;
```

您可以使用 dt 命令显示 JIT\_调试\_信息结构。

```dbgcmd
0: kd> dt JIT_DEBUG_INFO
nt!JIT_DEBUG_INFO
   +0x000 dwSize           : Uint4B
   +0x004 dwProcessorArchitecture : Uint4B
   +0x008 dwThreadID       : Uint4B
  +0x00c dwReserved0      : Uint4B
   +0x010 lpExceptionAddress : Uint8B
   +0x018 lpExceptionRecord : Uint8B
   +0x020 lpContextRecord  : Uint8B
```

**查看异常记录、 调用堆栈和 LastEvent 使用 WinDbg**

.Jdinfo 命令已用于将上下文设置到失败的时间点后，可以查看.jdinfo、 调用堆栈和 lastevent，返回的异常记录，如下所示，若要调查原因。

```dbgcmd
0:000> .jdinfo  0x00000000003E0000
----- Exception occurred on thread 0:15c8
ntdll!NtWaitForMultipleObjects+0x14:
00007ffc`81a959a4 c3              ret

----- Exception record at 00000000`003e0028:
ExceptionAddress: 00007ff791d81014 (CrashAV_x64!wmain+0x0000000000000014)
   ExceptionCode: c0000005 (Access violation)
  ExceptionFlags: 00000000
NumberParameters: 2
   Parameter[0]: 0000000000000001
   Parameter[1]: 0000000000000000
Attempt to write to address 0000000000000000
...

0:000> k
  *** Stack trace for last set context - .thread/.cxr resets it
# Child-SP          RetAddr           Call Site
00 00000000`006ff8b0 00007ff7`91d811d2 CrashAV_x64!wmain+0x14 [c:\my\my_projects\crash\crashav\crashav.cpp @ 14]
01 00000000`006ff8e0 00007ffc`7fa38364 CrashAV_x64!__tmainCRTStartup+0x11a [f:\dd\vctools\crt_bld\self_64_amd64\crt\src\crtexe.c @ 579]
02 00000000`006ff910 00007ffc`81a55e91 KERNEL32!BaseThreadInitThunk+0x14
03 00000000`006ff940 00000000`00000000 ntdll!RtlUserThreadStart+0x21

0:000> .lastevent
Last event: 153c.5d0: Break instruction exception - code 80000003 (first chance)
  debugger time: Thu Sep  8 12:55:08.968 2016 (UTC - 7:00)
```

 

 





