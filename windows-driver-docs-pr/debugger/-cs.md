---
title: cs
description: Cs 扩展插件都会显示一个或多个关键部分或整个关键部分树。
ms.assetid: 767ad508-013b-4cf7-808d-38ff64418879
keywords:
- cs Windows 调试
ms.date: 11/15/2018
topic_type:
- apiref
api_name:
- cs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f50f65fd8f710b6457e259d458d8aca995f0b394
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336874"
---
# <a name="cs"></a>!cs


**！ Cs**扩展插件都会显示一个或多个关键部分或整个关键部分树。

```dbgsyntax
!cs [-s] [-l] [-o] 
!cs [-s] [-o] Address 
!cs [-s] [-l] [-o] StartAddress EndAddress 
!cs [-s] [-o] -d InfoAddress 
!cs [-s] -t [TreeAddress] 
!cs -? 
```

## <a name="parameters"></a>Parameters

参数 | 描述
|---------|-------------|
**-s**  | 显示每个关键部分初始化堆栈跟踪，如果此信息可用。
**-l**  |显示仅锁定关键部分。
**-o**   |将显示为任何锁定的关键部分所显示的所有者的堆栈。
*地址* |指定要显示的关键部分的地址。 如果省略此参数，调试器将显示当前进程中的所有关键部分。
*StartAddress*   | 指定要搜索的关键节的地址范围的起始时间。
*EndAddress*   | 指定要搜索的关键节的地址范围的结束。
**-d**    | 显示与 DebugInfo 相关联的关键部分。
*InfoAddress*   | 指定 DebugInfo 的地址。
**-t**    | 显示关键部分树。 可以使用之前 **-t**选项，你必须激活[应用程序验证工具](application-verifier.md)目标进程然后选择**检查锁使用**选项。
*TreeAddress*    | 指定的关键部分树的根的地址。 如果省略此参数或指定为零，调试器会显示当前进程的关键部分树。
**-?**    | 显示此扩展中的一些帮助文本[调试器命令窗口](debugger-command-window.md)。

### <a name="dll"></a>DLL

Exts.dll
 

### <a name="additional-information"></a>其他信息

有关其他命令和扩展，可以显示关键部分的信息，请参阅[显示关键节](displaying-a-critical-section.md)。 有关临界区的详细信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 

#### <a name="remarks"></a>备注

**！ Cs**扩展需要完整的符号 （包括类型信息），正在调试的进程和 Ntdll.dll 的。 如果您没有 Ntdll.dll 的符号，请参阅[安装 Windows 符号文件](installing-windows-symbol-files.md)。

下面的示例演示如何使用 **！ cs**。 以下命令显示有关的信息关键部分地址 0x7803B0F8 处，并显示其初始化堆栈跟踪。

```dbgcmd
0:001> !cs -s 0x7803B0F8
Critical section   = 0x7803B0F8 (MSVCRT!__app_type+0x4)
DebugInfo          = 0x6A262080
NOT LOCKED
LockSemaphore      = 0x0
SpinCount          = 0x0

Stack trace for DebugInfo = 0x6A262080:

0x6A2137BD: ntdll!RtlInitializeCriticalSectionAndSpinCount+0x9B
0x6A207A4C: ntdll!LdrpCallInitRoutine+0x14
0x6A205569: ntdll!LdrpRunInitializeRoutines+0x1D9
0x6A20DCE1: ntdll!LdrpInitializeProcess+0xAE5
```

下面的命令显示有关其 DebugInfo 位于地址 0x6A262080 的关键部分的信息。

```dbgcmd
0:001> !cs -d 0x6A262080
DebugInfo          = 0x6A262080
Critical section   = 0x7803B0F8 (MSVCRT!__app_type+0x4)
NOT LOCKED
LockSemaphore      = 0x0
SpinCount          = 0x0
```

下面的命令显示当前进程中的所有活动的关键部分有关的信息。

```dbgcmd
## 0:001> !cs

DebugInfo          = 0x6A261D60
Critical section   = 0x6A262820 (ntdll!RtlCriticalSectionLock+0x0)
LOCKED
LockCount          = 0x0
OwningThread       = 0x460
RecursionCount     = 0x1
LockSemaphore      = 0x0
## SpinCount          = 0x0

DebugInfo          = 0x6A261D80
Critical section   = 0x6A262580 (ntdll!DeferedCriticalSection+0x0)
NOT LOCKED
LockSemaphore      = 0x7FC
## SpinCount          = 0x0

DebugInfo          = 0x6A262600
Critical section   = 0x6A26074C (ntdll!LoaderLock+0x0)
NOT LOCKED
LockSemaphore      = 0x0
## SpinCount          = 0x0

DebugInfo          = 0x77fbde20
Critical section   = 0x77c8ba60 (GDI32!semColorSpaceCache+0x0)
LOCKED
LockCount          = 0x0
OwningThread       = 0x00000dd8
RecursionCount     = 0x1
LockSemaphore      = 0x0
## SpinCount          = 0x00000000

...
```

以下命令显示的关键部分树。

```dbgcmd
0:001> !cs -t

Tree root 00bb08c0

Level     Node       CS    Debug  InitThr EnterThr  WaitThr TryEnThr LeaveThr EnterCnt  WaitCnt
## 


    0 00bb08c0 77c7e020 77fbcae0      4c8      4c8        0        0      4c8        c        0
 1 00dd6fd0 0148cfe8 01683fe0      4c8      4c8        0        0      4c8        2        0
 2 00bb0aa0 008e8b84 77fbcc20      4c8        0        0        0        0        0        0
    3 00bb09e0 008e8704 77fbcba0      4c8        0        0        0        0        0        0
    4 00bb0a40 008e8944 77fbcbe0      4c8        0        0        0        0        0        0
    5 00bb0a10 008e8824 77fbcbc0      4c8        0        0        0        0        0        0
    5 00bb0a70 008e8a64 77fbcc00      4c8        0        0        0        0        0        0
    3 00bb0b00 008e8dc4 77fbcc60      4c8        0        0        0        0        0        0
    4 00bb0ad0 008e8ca4 77fbcc40      4c8        0        0        0        0        0        0
    4 00bb0b30 008e8ee4 77fbcc80      4c8        0        0        0        0        0        0
    5 00dd4fd0 0148afe4 0167ffe0      4c8        0        0        0        0        0        0
    2 00bb0e90 77c2da98 00908fe0      4c8      4c8        0        0      4c8       3a        0
 3 00bb0d70 77c2da08 008fcfe0      4c8        0        0        0        0        0        0
```

以下各项显示在此 **！ cs-t**显示：

-   **InitThr**是初始化 CS 的线程的线程 ID。

-   **EnterThr**的调用的线程 id **EnterCriticalSection**上次的时间。

-   **WaitThr**找到关键部分，另一个线程的线程 ID 拥有和等待的时间它最后一次。

-   **TryEnThr**的调用的线程 id **TryEnterCriticalSection**上次的时间。

-   **LeaveThr**的调用的线程 id **LeaveCriticalSection**上次时间

-   **EnterCnt**是的计数**EnterCriticalSection**。

-   **WaitCnt**是争用计数。



 





