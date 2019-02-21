---
title: 显示关键节
description: 显示关键节
ms.assetid: d55971f6-9112-417d-8fb6-e299c7fc90a7
keywords:
- 关键节
- 关键节概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 625a4c5361746a3c3e56a3c1cc174b28c76dad20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533208"
---
# <a name="displaying-a-critical-section"></a>显示关键节


## <span id="ddk_displaying_a_critical_section_dbg"></span><span id="DDK_DISPLAYING_A_CRITICAL_SECTION_DBG"></span>


通过各种不同的方法，可以在用户模式下显示关键部分。 每个字段的确切含义取决于所使用的 Microsoft Windows 版本的版本。

### <a name="span-iddisplayingcriticalsectionsspanspan-iddisplayingcriticalsectionsspandisplaying-critical-sections"></a><span id="displaying_critical_sections"></span><span id="DISPLAYING_CRITICAL_SECTIONS"></span>显示关键部分

可以通过显示关键部分 **！ ntsdexts.locks**扩展， **！ critsec**扩展 **！ cs**扩展，和**dt （显示类型）** 命令。

[ **！ Ntsdexts.locks** ](-locks---ntsdexts-locks-.md)扩展显示与当前进程关联的关键部分的列表。 如果 **-v**选项，则会显示所有的关键部分。 下面是一个示例：

```dbgcmd
0:000> !locks

CritSec ntdll!FastPebLock+0 at 77FC49E0
LockCount          0
RecursionCount     1
OwningThread       c78
EntryCount         0
ContentionCount    0
*** Locked

....
Scanned 37 critical sections
```

如果您知道您想要显示的关键部分的地址，则可以使用[ **！ critsec** ](-critsec.md)扩展。 这将显示同一集合的信息作为 **！ ntsdexts.locks**。 例如：

```dbgcmd
0:000> !critsec 77fc49e0

CritSec ntdll!FastPebLock+0 at 77FC49E0
LockCount          0
RecursionCount     1
OwningThread       c78
EntryCount         0
ContentionCount    0
*** Locked
```

[ **！ Cs** ](-cs.md)扩展可以显示关键部分根据其地址、 搜索临界区的地址范围和甚至可以显示与每个关键部分关联的堆栈跟踪。 其中一些功能需要完整的 Windows 符号才能正常工作。 如果应用程序验证器处于活动状态， **！ cs-t**可用于显示关键部分树。 请参阅 **！ cs**参考页的详细信息和示例。

显示的信息 **！ cs**略有不同的情况下显示 **！ ntsdexts.locks**并 **！ critsec**。 例如：

```dbgcmd
## 0:000> !cs 77fc49e0

Critical section   = 0x77fc49e0 (ntdll!FastPebLock+0x0)
DebugInfo          = 0x77fc3e00
LOCKED
LockCount          = 0x0
OwningThread       = 0x00000c78
RecursionCount     = 0x1
LockSemaphore      = 0x0
SpinCount          = 0x00000000
```

[ **Dt （显示类型）** ](dt--display-type-.md)命令可以用于显示文本内容的 RTL\_严重\_部分结构。 例如：

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 77fc49e0
   +0x000 DebugInfo        : 0x77fc3e00 
   +0x004 LockCount        : 0
   +0x008 RecursionCount   : 1
   +0x00c OwningThread     : 0x00000c78 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

### <a name="span-idinterpretingcriticalsectionfieldsinwindowsxpandwindows2000spanspan-idinterpretingcriticalsectionfieldsinwindowsxpandwindows2000spaninterpreting-critical-section-fields-in-windows-xp-and-windows-2000"></a><span id="interpreting_critical_section_fields_in_windows_xp_and_windows_2000"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_XP_AND_WINDOWS_2000"></span>解释 Windows XP 中的关键部分字段和 Windows 2000

临界区结构的最重要的字段如下所示：

-   在 Microsoft Windows 2000 和 Windows XP **LockCount**字段指示的任何线程调用的次数**EnterCriticalSection**例程此关键部分，减一。 此字段起步价为-1，表示未锁定的关键部分。 每次调用**EnterCriticalSection**增加此值; 每个调用**LeaveCriticalSection**递减它。 例如，如果**LockCount**为 5、 锁定此关键部分、 一个线程已获取它，和五个其他线程等待该锁定。

-   **RecursionCount**字段指示拥有线程已调用的次数**EnterCriticalSection**此关键部分。

-   **EntryCount**字段指示的所属的线程以外的线程已调用的次数**EnterCriticalSection**此关键部分。

新初始化的关键部分如下所示：

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          NOT LOCKED 
RecursionCount     0
OwningThread       0
EntryCount         0
ContentionCount    0
```

调试器将显示"未锁定"的值作为**LockCount**。 解锁的关键部分此字段的实际值为-1。 你可以验证这一点与**dt （显示类型）** 命令：

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 433e60
   +0x000 DebugInfo        : 0x77fcec80
   +0x004 LockCount        : -1
   +0x008 RecursionCount   : 0
   +0x00c OwningThread     : (null) 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

当第一个线程调用**EnterCriticalSection**例程，关键节**LockCount**， **RecursionCount**， **EntryCount**并**ContentionCount**字段递增 1，并**OwningThread**变得调用方的线程 ID。 **EntryCount**并**ContentionCount**是永远不会减少。 例如：

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          0
RecursionCount     1
OwningThread       4d0
EntryCount         0
ContentionCount    0
```

此时，会出现四个不同的状况。

1.  所属的线程调用**EnterCriticalSection**试。 这将增大**LockCount**并**RecursionCount**。 **EntryCount**不会增加。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     2
    OwningThread       4d0
    EntryCount         0
    ContentionCount    0
    ```

2.  不同的线程调用**EnterCriticalSection**。 这将增大**LockCount**并**EntryCount**。 **RecursionCount**不会增加。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     1
    OwningThread       4d0
    EntryCount         1
    ContentionCount    1
    ```

3.  所属的线程调用**LeaveCriticalSection**。 这将递减**LockCount** （为-1) 和**RecursionCount** （为 0)，并将重置**OwningThread**为 0。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          NOT LOCKED 
    RecursionCount     0
    OwningThread       0
    EntryCount         0
    ContentionCount    0
    ```

4.  另一个线程调用**LeaveCriticalSection**。 这将产生与所属的线程调用相同的结果**LeaveCriticalSection** -它会递减**LockCount** （为-1) 和**RecursionCount** （为 0)，并将重置**OwningThread**为 0。

如果任何线程调用**LeaveCriticalSection**，Windows 递减**LockCount**并**RecursionCount**。 此功能具有好坏两方面。 它允许在一个线程进入关键节并将关键部分保留在另一个线程上的设备驱动程序。 但是，它还使它可能会意外地调用**LeaveCriticalSection**对错误线程，或调用**LeaveCriticalSection**太多时间和原因**LockCount**到达值小于-1。 这将损坏了关键部分，并导致无限期等待关键部分的所有线程。

### <a name="span-idinterpretingcriticalsectionfieldsinwindowsserver2003sp1andlaspanspan-idinterpretingcriticalsectionfieldsinwindowsserver2003sp1andlaspaninterpreting-critical-section-fields-in-windows-server-2003-sp1-and-later"></a><span id="interpreting_critical_section_fields_in_windows_server_2003_sp1_and_la"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_SERVER_2003_SP1_AND_LA"></span>解释在 Windows Server 2003 SP1 及更高版本的关键部分字段

在 Microsoft Windows Server 2003 Service Pack 1 和更高版本的 Windows， **LockCount**字段进行分析，如下所示：

-   最低位显示锁定状态。 如果此位为 0，已锁定关键部分;如果为 1，未锁定关键部分。

-   下一位显示是否已为此锁唤醒线程。 如果此位为 0，然后在线程具有已唤醒此锁;如果为 1，任何线程都具有已不唤醒。

-   剩余的位是 1 的补数的等待锁的线程数。

例如，假设**LockCount**是-22。 可以按这种方式确定最低位：

```dbgcmd
0:009> ? 0x1 & (-0n22)
Evaluate expression: 0 = 00000000
```

以这种方式，可以确定下一步最低位：

```dbgcmd
0:009> ? (0x2 & (-0n22)) >> 1
Evaluate expression: 1 = 00000001
```

可以按这种方式确定剩余的位 1 的补数：

```dbgcmd
0:009> ? ((-1) - (-0n22)) >> 2
Evaluate expression: 5 = 00000005
```

在此示例中，第一位是 0，因此锁定关键部分。 第二个位是 1，并因此将没有线程唤醒此锁。 剩余的位求补为 5，，因此有五个线程在等待此锁。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何调试临界区的超时的信息，请参阅[关键部分超时](critical-section-time-outs.md)。 有关临界区的常规信息，请参阅 Microsoft Windows SDK，Windows Driver Kit (WDK) 或*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 





