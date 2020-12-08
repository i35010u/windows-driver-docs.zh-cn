---
title: 资源超时
description: 资源超时
keywords:
- 资源超时
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29520469c3d7fd1331ba9b4b9771e674bd46cbef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816933"
---
# <a name="resource-time-outs"></a>资源超时


## <span id="ddk_resource_time_outs_dbg"></span><span id="DDK_RESOURCE_TIME_OUTS_DBG"></span>


在资源超时时，等待资源的线程将中断内核调试器，其中包含类似于以下内容的消息：

```console
Resource @ 800e99c0
 ActiveCount = 0001  Flags = IsOwnedExclusive sharedWaiter
 NumberOfExclusiveWaiters = 0000
  Thread = 809cd2f0, Count = 01
  Thread = 809ebc50, Count = 01
  Thread = 00000000, Count = 00
  Thread = 00000000, Count = 00
  Thread = 00000000, Count = 00
NT!DbgBreakPoint+0x4:
800cee04: 000000ad callkd 
```

持有锁的线程是 (或多个线程中列出的第一个线程（如果它是共享锁) ）。 若要检查该线程，请在前面的示例 **中的线程** ID (809cd2f0，) 。 这会为拥有该资源的线程提供一个堆栈。 如果它也在等待资源变为可用，则 **ExpWaitForResourceExclusive** 函数或 **ExpWaitForResourceShared** 函数将在该线程的堆栈上。

**ExpWaitForResource * Xxx*** 的第一个参数是正在等待的锁。 若要了解该资源，请使用 **！锁 &lt; *资源 id* &gt;** 扩展，这将为你提供另一个线程来进行检查。

如果到达不等待其他资源的线程，则该线程可能是问题的根源。 有关所有持有锁的列表，请在 **&gt; kd** 提示符处使用不带参数的 **！锁** 扩展。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

```console
Resource @ fc664ee0                  // Here's the resource lock address

 ActiveCount = 0001  Flags = IsOwnedExclusive ExclusiveWaiter
 NumberOfExclusiveWaiters = 0001
  Thread = ffaf5410, Count = 01                // Here's the owning thread
  Thread = 00000000, Count = 00
ntoskrnl!_DbgBreakPoint:
80131400 cc               int     3

kd> kb                                        // Start with a stack
ChildEBP RetAddr  Args to Child
fcd44980 801154c0 fc664ee0 ffab45d0 00110001 ntoskrnl!_DbgBreakPoint
fcd4499c 80102521 fc664ee0 ffb08ea8 fcd44a4c ntoskrnl!_ExpWaitForResource+0x114        // Lock being waited on...

fcd449e8 fc6509fa e12597c8 fef27c08 fee4fca8 ntoskrnl!_ExAcquireResourceExclusiveLite+0xa5
00380020 00000000 00000000 00000000 00000000 nwrdr!_CreateScb+0x2ff

kd> !locks fc664ee0                      // !locks resource address gives lock info
Resource @ nwrdr!_NwScavengerSpinLock (0xfc664ee0)    Exclusively owned
    Contention Count = 45
    NumberOfExclusiveWaiters = 1
     Threads: ffaf5410-01                  // Owning thread again
1 total locks, 1 locks currently held

kd> !thread ffaf5410                     // Check the owning thread

THREAD ffaf5410  Cid e7.e8  Teb: 7ffde000 WAIT: (Executive) KernelMode Non-Alertable
    feecf698  SynchronizationEvent
IRP List:
    fef29208: (0006,00b8) Flags: 00000884  Mdl: feed8328
Not impersonating
Owning Process ffaf5690
WaitTime (seconds)      2781250
Context Switch Count    183175
UserTime                  0:00:23.0153
KernelTime                0:01:01.0187
Start Address 0x77f04644
Initial Sp fec6c000 Current Sp fec6b938
Priority 11 BasePriority 7 PriorityDecrement 0 DecrementCount 8

ChildEBP RetAddr  Args to Child
fec6b950 801044fc feecf668 feecf668 00000080 ntoskrnl!KiSwapContext+0x25
fec6b974 fc655976 feecf698 00000000 00000000 ntoskrnl!_KeWaitForSingleObject+0x218
fec6ba5c fc6509fa e1263968 fef29208 feecf668 nwrdr!_ExchangeWithWait+0x38
fec6ba28 fc6533e5 feecf668 e125b3c8 ffafae08 nwrdr!_CreateScb+0x2ff
fec6bac0 fc652f26 feecf668 fec6bae4 fef29208 nwrdr!_CreateRemoteFile+0x2c9
fec6bb6c fc652b14 feecf668 fef29208 fee50b60 nwrdr!_NwCommonCreate+0x3a2

fec6bbac 80107aea fee50b60 fef29208 804052ac nwrdr!_NwFsdCreate+0x56
fec6bbc0 80142792 fef37700 fec6bdbc fee50b28 ntoskrnl!IofCallDriver+0x38
fec6bd10 80145403 fee50b60 00000000 fec6bdbc ntoskrnl!_IopParseDevice+0x6a0
fec6bd7c 80144c0c 00000000 fec6be34 00000040 ntoskrnl!_ObpLookupObjectName+0x479
fec6be5c 80127803 0012dd64 00000000 80127701 ntoskrnl!_ObOpenObjectByName+0xa2
fec6bef4 801385c3 0012dd64 0012dd3c 00000000 ntoskrnl!_NtQueryAttributesFile+0xc1
fec6bef4 77f716ab 0012dd64 0012dd3c 00000000 ntoskrnl!_KiSystemService+0x83

0012dd20 00000000 00000000 00000000 00000000 ntdll!_ZwQueryAttributesFile+0xb 
```

 

 





