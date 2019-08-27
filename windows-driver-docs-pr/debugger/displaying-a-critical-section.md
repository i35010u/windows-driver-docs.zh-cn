---
title: 显示关键节
description: 显示关键节
ms.assetid: d55971f6-9112-417d-8fb6-e299c7fc90a7
keywords:
- 关键部分
- 关键部分概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8de3960552ca94b1f53e30f741bbcd16ba4a14ba
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025313"
---
# <a name="displaying-a-critical-section"></a>显示关键节


## <span id="ddk_displaying_a_critical_section_dbg"></span><span id="DDK_DISPLAYING_A_CRITICAL_SECTION_DBG"></span>


可以通过多种不同的方法在用户模式下显示关键部分。 每个字段的确切含义取决于所使用的 Microsoft Windows 版本。

### <a name="span-iddisplaying_critical_sectionsspanspan-iddisplaying_critical_sectionsspandisplaying-critical-sections"></a><span id="displaying_critical_sections"></span><span id="DISPLAYING_CRITICAL_SECTIONS"></span>显示关键部分

临界区可以通过 **! ntsdexts**扩展、 **! critsec**扩展、 **! .Cs**扩展和**dt (显示类型)** 命令来显示。

[ **! Ntsdexts**](-locks---ntsdexts-locks-.md) extension 显示与当前进程相关联的关键部分的列表。 如果使用了 **-v**选项, 将显示所有关键部分。 下面是一个示例：

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

如果知道要显示的关键部分的地址, 可以使用[ **! critsec**](-critsec.md)扩展名。 这将显示与 **! ntsdexts**相同的信息集合。 例如：

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

[ **! Cs**](-cs.md)扩展可以根据其地址显示关键部分, 在 "关键" 部分的地址范围内搜索, 甚至显示与每个关键部分关联的堆栈跟踪。 其中一些功能需要完整的 Windows 符号才能正常工作。 如果应用程序验证工具处于活动状态, 则 **! cs-t**可用于显示关键部分树。 有关详细信息和示例, 请参阅 **! cs**参考页。

通过 **!** **ntsdexts**和 **! critsec**显示的信息略有不同。 例如：

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

[**Dt (显示类型)** ](dt--display-type-.md)命令可用于显示 RTL\_临界\_区结构的文本内容。 例如：

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 77fc49e0
   +0x000 DebugInfo        : 0x77fc3e00 
   +0x004 LockCount        : 0
   +0x008 RecursionCount   : 1
   +0x00c OwningThread     : 0x00000c78 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

### <a name="span-idinterpreting_critical_section_fields_in_windows_xp_and_windows_2000spanspan-idinterpreting_critical_section_fields_in_windows_xp_and_windows_2000spaninterpreting-critical-section-fields-in-windows-xp-and-windows-2000"></a><span id="interpreting_critical_section_fields_in_windows_xp_and_windows_2000"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_XP_AND_WINDOWS_2000"></span>在 Windows XP 和 Windows 2000 中解释关键部分字段

关键部分结构的最重要字段如下所示:

-   在 Microsoft Windows 2000 和 Windows XP 中, " **LockCount** " 字段指示任何线程为此临界区 (减 1) 调用**EnterCriticalSection**例程的次数。 对于解锁的关键部分, 此字段从-1 开始。 **EnterCriticalSection**的每次调用都会递增此值;**LeaveCriticalSection**的每次调用都会将其递减。 例如, 如果**LockCount**为 5, 则锁定此关键部分, 一个线程已获取它, 另外5个线程正在等待此锁定。

-   **RecursionCount**字段指示拥有线程为此关键部分调用**EnterCriticalSection**的次数。

-   **EntryCount**字段指示除所属线程之外的其他线程为此关键部分调用**EnterCriticalSection**的次数。

新初始化的关键部分如下所示:

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          NOT LOCKED 
RecursionCount     0
OwningThread       0
EntryCount         0
ContentionCount    0
```

调试器显示 "未锁定" 作为**LockCount**的值。 解锁关键部分的此字段的实际值为-1。 可以通过**dt (显示类型)** 命令验证此内容:

```dbgcmd
0:000> dt RTL_CRITICAL_SECTION 433e60
   +0x000 DebugInfo        : 0x77fcec80
   +0x004 LockCount        : -1
   +0x008 RecursionCount   : 0
   +0x00c OwningThread     : (null) 
   +0x010 LockSemaphore    : (null) 
   +0x014 SpinCount        : 0
```

当第一个线程调用**EnterCriticalSection**例程时, 临界区的**LockCount**、 **RecursionCount**、 **EntryCount**和**ContentionCount**字段都将递增 1, 而**OwningThread**成为调用方的线程 ID。 **EntryCount**和**ContentionCount**永远不会减少。 例如：

```dbgcmd
0:000> !critsec 433e60
CritSec mymodule!cs+0 at 00433E60
LockCount          0
RecursionCount     1
OwningThread       4d0
EntryCount         0
ContentionCount    0
```

此时, 可能出现四个不同的情况。

1.  拥有线程再次调用**EnterCriticalSection** 。 这会增加**LockCount**和**RecursionCount**。 **EntryCount**不会增加。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     2
    OwningThread       4d0
    EntryCount         0
    ContentionCount    0
    ```

2.  另一个线程调用**EnterCriticalSection**。 这会增加**LockCount**和**EntryCount**。 **RecursionCount**不会增加。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          1
    RecursionCount     1
    OwningThread       4d0
    EntryCount         1
    ContentionCount    1
    ```

3.  拥有线程调用**LeaveCriticalSection**。 这会将**LockCount** (到-1) 和**RecursionCount** (到 0) 减, 并将**OwningThread**重置为0。

    ```dbgcmd
    0:000> !critsec 433e60
    CritSec mymodule!cs+0 at 00433E60
    LockCount          NOT LOCKED 
    RecursionCount     0
    OwningThread       0
    EntryCount         0
    ContentionCount    0
    ```

4.  另一个线程调用**LeaveCriticalSection**。 这会生成与调用**LeaveCriticalSection**的所属线程相同的结果--它将减少**LockCount** (到-1) 和**RecursionCount** (到 0), 并将**OwningThread**重置为0。

当任何线程调用**LeaveCriticalSection**时, Windows 将减少**LockCount**和**RecursionCount**。 此功能具有良好和不良的方面。 它允许设备驱动程序在一个线程上输入临界区, 并在另一个线程上保留临界区。 不过, 它还可以在错误的线程上意外调用**LeaveCriticalSection** , 或调用**LeaveCriticalSection**的次数过多, 从而导致**LockCount**达到小于-1 的值。 这会损坏关键部分, 并导致所有线程无限期地等待关键部分。

### <a name="span-idinterpreting_critical_section_fields_in_windows_server_2003_sp1_and_laspanspan-idinterpreting_critical_section_fields_in_windows_server_2003_sp1_and_laspaninterpreting-critical-section-fields-in-windows-server-2003-sp1-and-later"></a><span id="interpreting_critical_section_fields_in_windows_server_2003_sp1_and_la"></span><span id="INTERPRETING_CRITICAL_SECTION_FIELDS_IN_WINDOWS_SERVER_2003_SP1_AND_LA"></span>解释 Windows Server 2003 SP1 及更高版本中的关键部分字段

在 Microsoft Windows Server 2003 Service Pack 1 和更高版本的 Windows 中, 按如下方式分析**LockCount**字段:

-   最小位显示锁定状态。 如果此位为 0, 则锁定关键部分;如果为 1, 则不会锁定临界区。

-   下一位显示线程是否已唤醒此锁。 如果此位为 0, 则表示线程已唤醒此锁;如果为 1, 则尚未唤醒线程。

-   其余位是等待锁的线程数的补码。

例如, 假设**LockCount**为-22。 可以通过以下方式确定最低位:

```dbgcmd
0:009> ? 0x1 & (-0n22)
Evaluate expression: 0 = 00000000
```

可以通过以下方式确定下一小数位:

```dbgcmd
0:009> ? (0x2 & (-0n22)) >> 1
Evaluate expression: 1 = 00000001
```

可以通过以下方式确定剩余位的补码:

```dbgcmd
0:009> ? ((-1) - (-0n22)) >> 2
Evaluate expression: 5 = 00000005
```

在此示例中, 第一个位为 0, 因此临界区被锁定。 第二个位为 1, 因此没有为此锁唤醒任何线程。 剩余位的补码是 5, 因此有五个等待此锁定的线程。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何调试关键节超时的信息, 请参阅[临界区](critical-section-time-outs.md)超时。 有关关键部分的一般信息, 请参阅 "Microsoft Windows SDK、Windows 驱动程序工具包 (WDK) 或*Microsoft Windows 内部*Russinovich, 并将其标记为"

 

 





