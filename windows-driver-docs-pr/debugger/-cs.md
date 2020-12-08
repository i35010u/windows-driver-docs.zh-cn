---
title: cs
description: Cs 扩展显示一个或多个关键部分或整个关键部分树。
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
ms.openlocfilehash: d0cc0b30872d6301ee077c41a920debc536d7434
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803325"
---
# <a name="cs"></a>!cs


**！ Cs** 扩展显示一个或多个关键部分或整个关键部分树。

```dbgsyntax
!cs [-s] [-l] [-o] 
!cs [-s] [-o] Address 
!cs [-s] [-l] [-o] StartAddress EndAddress 
!cs [-s] [-o] -d InfoAddress 
!cs [-s] -t [TreeAddress] 
!cs -? 
```

## <a name="parameters"></a>参数

参数 | 描述
|---------|-------------|
**-s**  | 如果此信息可用，则显示每个关键节的初始化堆栈跟踪。
**-l**  |仅显示锁定的关键部分。
**-o**   |显示所显示的任何锁定关键部分的所有者堆栈。
*Address* |指定要显示的关键部分的地址。 如果省略此参数，则调试器将显示当前进程中的所有关键部分。
*StartAddress*   | 指定要在关键部分中搜索的地址范围的起始位置。
*EndAddress*   | 指定要在关键部分中搜索的地址范围的结尾。
**-d**    | 显示与 DebugInfo 相关联的关键部分。
*InfoAddress*   | 指定 DebugInfo 的地址。
**-t**    | 显示临界区树。 必须先激活目标进程 [应用程序验证工具](../devtest/application-verifier.md)，然后选择 "**检查锁使用情况**" 选项，然后才能使用 **-t** 选项。
*TreeAddress*    | 指定临界区树的根地址。 如果省略此参数或指定零，则调试器将显示当前进程的关键部分树。
**-?**    | 在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本。

### <a name="dll"></a>DLL

Exts.dll
 

### <a name="additional-information"></a>其他信息

有关可显示关键部分信息的其他命令和扩展，请参阅 [显示关键部分](displaying-a-critical-section.md)。 有关关键部分的详细信息，请参阅 "Microsoft Windows SDK 文档"、"Windows 驱动程序工具包" (WDK) 文档和 *Microsoft Windows 内部* 的 "标记 Russinovich" 和 "David"。 

#### <a name="remarks"></a>备注

**！ Cs** 扩展需要完整符号 (包括要调试的进程的类型信息) 和 Ntdll.dll。 如果没有 Ntdll.dll 的符号，请参阅 [安装 Windows 符号文件](installing-windows-symbol-files.md)。

下面的示例演示如何使用 **！ cs**。 下面的命令显示有关地址0x7803B0F8 的关键部分的信息并显示其初始化堆栈跟踪。

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

以下命令显示有关其 DebugInfo 位于 address 0x6A262080 的临界区的信息。

```dbgcmd
0:001> !cs -d 0x6A262080
DebugInfo          = 0x6A262080
Critical section   = 0x7803B0F8 (MSVCRT!__app_type+0x4)
NOT LOCKED
LockSemaphore      = 0x0
SpinCount          = 0x0
```

以下命令显示有关当前进程中的所有活动关键部分的信息。

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

以下命令显示临界区树。

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

此项中显示了以下各项： **cs-t** 显示：

-   **InitThr** 是初始化 CS 的线程的线程 ID。

-   **EnterThr** 是上次调用 **EnterCriticalSection** 的线程的 ID。

-   **WaitThr** 是一个线程的 ID，该 ID 找到了另一个线程最后一次拥有并等待的关键部分。

-   **TryEnThr** 是上次调用 **TryEnterCriticalSection** 的线程的 ID。

-   **LeaveThr** 是上次调用 **LeaveCriticalSection** 的线程的 ID

-   **EnterCnt** 是 **EnterCriticalSection** 的计数。

-   **WaitCnt** 是争用计数。



