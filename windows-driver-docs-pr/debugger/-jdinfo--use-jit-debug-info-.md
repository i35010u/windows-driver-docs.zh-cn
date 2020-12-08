---
title: .jdinfo（使用 JIT_DEBUG_INFO）
description: Jdinfo 命令使用 JIT_DEBUG_INFO 结构作为异常的源，并使用 (JIT) 调试的实时上下文。
keywords:
- 使用 JIT_DEBUG_INFO () 命令-----附录
- JIT_DEBUG_INFO-----附录
- jdinfo (使用 JIT_DEBUG_INFO) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .jdinfo (Use JIT_DEBUG_INFO)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 46c57f7c62641682275b64954bd5bceaae2f659f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827363"
---
# <a name="jdinfo-use-jit_debug_info"></a>jdinfo (使用 JIT \_ 调试 \_ 信息) 


**Jdinfo** 命令使用 jit \_ 调试 \_ 信息结构作为异常的源，并使用 jit) 调试的实时 (上下文。 使用 AeDebug 注册表项中指定的% p 参数将结构的地址传递给 **jdinfo** 命令。

有关使用的注册表项的详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。 有关注册上下文的详细信息，请参阅 [更改上下文](changing-contexts.md)。

```dbgcmd
.jdinfo Address 
```

## <a name="span-idddk_apc_meta_use_jit_debug_info_dbgspanspan-idddk_apc_meta_use_jit_debug_info_dbgspanparameters"></a><span id="ddk_apc_meta_use_jit_debug_info_dbg"></span><span id="DDK_APC_META_USE_JIT_DEBUG_INFO_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 JIT \_ 调试信息结构的地址 \_ 。 使用 AeDebug 注册表项中指定的% p 参数将结构的地址传递给 **jdinfo** 命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式</p></td>
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

 

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例

此示例演示如何将 AeDebug 注册表项配置为使用 WinDbg 作为 JIT 调试器。

```dbgcmd
Debugger = "Path\WinDbg.EXE -p %ld -e %ld -c ".jdinfo 0x%p"
```

然后，当发生崩溃时，将调用配置的 JIT 调试器，并使用% p 参数将 JIT 调试信息结构的地址传递给在 \_ \_ 启动调试器后执行的 **jdinfo** 命令。

```dbgcmd
nMicrosoft (R) Windows Debugger Version 10.0.10240.9 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

**_ wait with pending attach
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

*Jdinfo** 命令使用 Windows Vista 中引入的 **AeDebug** 注册表信息。 有关使用的注册表项的详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。 **Jdinfo** 命令采用 \_ \_ 系统为 **AeDebug** 设置的 JIT 调试信息的地址，并将上下文设置为导致崩溃的异常。

可以在 **AeDebug** 中使用 **jdinfo** 命令而不是 **-g** ，使调试器设置为 **AeDebug** 状态，而无需执行。

此状态可能很有利，因为在通常情况下，出现用户模式异常时，将发生以下序列：

1.  Microsoft Windows 操作系统停止执行应用程序。

2.  已启动事后调试器。

3.  调试器附加到应用程序。

4.  调试器发出 "中转" 命令。  (此命令的原因是 **AeDebug** 键中的 **-g** 。 ) 

5.  目标尝试执行，可能会也可能不会遇到相同的异常。

6.  此异常中断调试器。

由于以下事件，可能会出现几个问题：

-   异常并不总是重复，这可能是因为在异常重新启动时已不再存在暂时性的情况。

-   可能会发生另一个事件，例如不同的异常。 无法知道它是否与原始事件完全相同。

-   附加调试器涉及注入新线程，如果线程持有加载程序锁，则可以阻止该线程。 注入新线程可能是此过程的重要干扰。

如果在 **AeDebug** 键中使用 **-jdinfo** 而不是 **-g** ，则不会执行任何操作。 相反，将 \_ \_ 使用% p 变量从 JIT 调试信息结构中检索异常信息。

例如，请看下面的 **AeDebug** 键。

```dbgcmd
ntsd -p %ld -e %ld -c ".jdinfo 0x%p"
```

下面的示例更不具侵害性。 **-Pv** 开关使调试器附加 noninvasively，而不会将任何新线程注入目标。

```dbgcmd
ntsd -pv -p %ld -e %ld -c ".jdinfo 0x%p"
```

如果使用此 noninvasive 选项，则退出调试器不会结束进程。 可以使用 [**kill (Kill 进程)**](-kill--kill-process-.md) 命令结束进程。

如果要将此用于转储文件调试，则在创建转储文件时，应使用 [**. 转储/j**](-dump--create-dump-file-.md) 将 JIT \_ 调试 \_ 信息结构添加到转储文件。

JIT \_ 调试 \_ 信息结构的定义如下。

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

可以使用 dt 命令来显示 JIT \_ 调试 \_ 信息结构。

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

**使用 WinDbg 查看异常记录、调用 Stack 和 LastEvent**

使用 jdinfo 命令将上下文设置为失败时间之后，可以查看由 jdinfo、调用堆栈和 lastevent 返回的异常记录，如以下所示，调查原因。

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

 

 





