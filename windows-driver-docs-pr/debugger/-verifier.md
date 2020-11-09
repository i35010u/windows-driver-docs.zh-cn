---
title: verifier
description: 验证程序扩展显示驱动程序验证程序及其操作的状态。
ms.assetid: e84993e1-da10-4041-8fc7-7f40806ee454
keywords:
- 驱动程序验证程序
- 验证程序 Windows 调试
ms.date: 05/03/2018
topic_type:
- apiref
api_name:
- verifier
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e4d27c04249aead17cc7c1b1b5f35e40288efc12
ms.sourcegitcommit: 2244845d5c74f5d260de1e1a994ae3cdcfaaa90a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2020
ms.locfileid: "94386078"
---
# <a name="verifier"></a>!verifier


**！ Verifier** 扩展显示驱动程序验证程序及其操作的状态。

驱动程序验证程序包含在 Windows 中。 它适用于已检查和免费的生成。 有关驱动程序验证程序的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档中的 [驱动程序验证程序](../devtest/driver-verifier.md) 主题。

语法

```dbgcmd
!verifier [Flags [Image]] 
!verifier 4 [Quantity] 
!verifier 8 [Quantity]  
!verifier 0x40 [Quantity] 
!verifier 0x80 [Quantity]
!verifier 0x80 Address
!verifier 0x100 [Quantity]
!verifier 0x100 Address
!verifier 0x200 [Address]
!verifier 0x400 [Address]
!verifier -disable
!verifier ?
```

## <a name="span-idddk__verifier_dbgspanspan-idddk__verifier_dbgspanparameters"></a><span id="ddk__verifier_dbg"></span><span id="DDK__VERIFIER_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定此命令的输出中显示的信息。 如果 *Flags* 等于值4、8、0x20、0x40、0x80 或0x100，则将根据与这些值关联的特定参数解释 **！ verifier** 的其余参数。 如果 *Flags* 等于任何其他值，即使设置了其中的一个或多个位，也只允许使用 *flags* 和 *Image* 参数。 *标志* 可以是以下位的任意总和;默认值为0：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
显示要验证的所有驱动程序的名称。 还显示了当前从非分页池和分页池分配给每个驱动程序的字节数。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
显示有关池大小、标头和池标记 (池的信息，以及卸载的驱动程序剩余) 和未处理的内存分配。 除非同时设置了位 0 (0x1) ，否则此标志不起作用。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
显示错误注入信息。 显示请求地址、符号名称和请求每个分配的代码的置换。 如果 *Flags* 正好是0x4 并且包含了 *数量* 参数，则可以选择所显示的这些记录的数量。 否则，会显示四条记录。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
显示所验证的驱动程序所做的最新的 IRQL 更改。 将显示旧的 IRQL、新的 IRQL、处理器和时间戳。 如果 *Flags* 正好是0x8 并且包含了 *数量* 参数，则可以选择所显示的这些记录的数量。 否则，会显示四条记录。

**警告**  在64位版本的 Windows 中，某些引发或降低 IRQL 的内核函数实现为内联代码，而不是导出函数。 驱动程序验证程序不报告内联代码所做的 IRQL 更改，因此驱动程序验证程序生成的 IRQL 转换日志可能是不完整的。 有关缺少的 IRQL 转换条目的示例，请参阅备注。

 

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 (0x40)   
 (Windows Vista 和更高版本) 显示驱动程序验证程序的 " **强制挂起 I/o 请求** " 选项中的信息，包括来自强制挂起的 irp 日志的跟踪。

*数量* 参数指定要显示的跟踪数。 默认情况下，将显示整个日志。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>第7位 (0x80)   
 (Windows Vista 及更高版本) 显示来自内核池分配/可用日志的信息。

*数量* 参数指定要显示的跟踪数。 默认情况下，将显示整个日志。

如果指定 *address* ，则只显示与内核池分配/可用日志中指定地址相关联的跟踪。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)   
 (Windows Vista 和更高版本) 显示 IoAllocateIrp、IoCompleteRequest 和 IoCancelIrp 调用日志中的信息。

数量参数指定要显示的跟踪数。 默认情况下，将显示整个日志。

如果指定 *Address* ，则只显示与指定 IRP 地址相关联的跟踪。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>第 9 (0x200)   
 (Windows Vista 及更高版本) 显示关键区域日志中的条目。

如果指定 *Address* ，则只显示与指定线程地址关联的条目。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>位 10 (0x400)   
 (Windows Vista 及更高版本) 显示驱动程序验证程序当前正在监视的已取消 Irp。

如果指定 *address* ，则只显示具有指定地址的 IRP。

<span id="Bit_11__0x800_"></span><span id="bit_11__0x800_"></span><span id="BIT_11__0X800_"></span>位 11 (0x800)   
 (Windows 8.1 和更高版本) 显示错误注入日志中的条目，该日志是在选择 " [系统低资源模拟](../devtest/systematic-low-resource-simulation.md) " 选项时创建的。

<span id="_______Image______"></span><span id="_______image______"></span><span id="_______IMAGE______"></span>*图像*   
如果使用 *标志* ，且不等于4、8或0x10，则 *映像* 将指定驱动程序的名称。 *Image* 用于筛选由 "0x1" 和 "0X2" *标志* 值显示的信息：仅考虑指定的驱动程序。 当前必须验证此驱动程序。

<span id="_______Quantity______"></span><span id="_______quantity______"></span><span id="_______QUANTITY______"></span>*数量*   
如果 *Flags* 与0x4 完全相等，则 " *数量* " 指定要显示的故障注入记录数。 如果 *Flags* 与0x8 完全相等，则 " *数量* " 指定要显示的 IRQL 日志条目数。 如果 *Flags* 完全等于0x40，则 " *数量* " 指定从强制挂起的 irp 日志中显示的跟踪数。 如果 Flags 完全等于0x80，则 "数量" 指定从内核池分配/空闲日志显示的跟踪数。 如果 Flags 完全等于0x100，则 "数量" 指定从 IoAllocateIrp、IoCompleteRequest 和 IoCancelIrp 调用日志中显示的跟踪数。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span>**-disable**   
清除调试目标上的当前驱动程序验证程序设置。 清除这些设置不会在重新启动后保持。 如果需要禁用 Driver Verifier 设置才能成功启动，请在 nt 上设置断点！VerifierInitSystem 并在此时使用 **！ verifier-disable** 命令。

<span id="______________"></span> **?**   
在调试器命令窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 [驱动程序验证程序](../devtest/driver-verifier.md)的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。


<a name="remarks"></a>注解
-------

下面的示例演示在64位版本的 Windows 上，IRQL 转换日志并非始终完成。 显示的两个条目是处理器2的日志中的连续条目。 第一项显示从2到0的 IRQL。 第二项显示从2到2的 IRQL。 缺少 IRQL 从0到2的情况的信息。

```dbgcmd
Thread:             fffffa80068c9400
Old irql:           0000000000000002
New irql:           0000000000000000
Processor:          0000000000000002
Time stamp:         0000000000000857

    fffff8800140f12a ndis!ndisNsiGetInterfaceInformation+0x20a
    fffff88001509478 NETIO!NsiGetParameterEx+0x178
    fffff88005f062f2 nsiproxy!NsippGetParameter+0x24a
    fffff88005f086db nsiproxy!NsippDispatchDeviceControl+0xa3
    fffff88005f087a0 nsiproxy!NsippDispatch+0x48

Thread:             fffffa80068c9400
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000002
Time stamp:         0000000000000857

    fffff8800140d48d ndis!ndisReferenceTopMiniportByNameForNsi+0x1ce
    fffff8800140f072 ndis!ndisNsiGetInterfaceInformation+0x152
    fffff88001509478 NETIO!NsiGetParameterEx+0x178
    fffff88005f062f2 nsiproxy!NsippGetParameter+0x24a
    fffff88005f086db nsiproxy!NsippDispatchDeviceControl+0xa3
```

4、8和0x20、0x40、0x80 和0x100 的值是 *标记* 的特殊值。 如果使用这些值，则可以使用 " **参数** " 部分中列出的特殊参数，而显示内容将只包含与该标志值相关联的信息。

如果使用 *标志* 的任何其他值，即使设置了其中的一个或多个位，也只允许使用 *flags* 和 *Image* 参数。 在这种情况下，除了显示的所有其他信息外， **！ verifier** 还会显示处于活动状态的驱动程序验证程序选项，以及有关池分配、IRQL 引发、旋转锁和剪裁的统计信息。

如果 *Flags* 等于0x20，则驱动程序验证程序的驱动程序挂起验证选项将使用为 *CompletionTime* 、 *CancelTime* 和 *ForceCancellation* 指定的值。 这些新值会立即生效，最后一次启动。 重新启动时，它们会恢复为默认值。

此外，如果 *标志* 等于 0x20 (有或不包含附加参数) ，则将打印驱动程序挂起验证日志。 有关解释该日志的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档中的驱动程序验证程序文档的驱动程序挂起验证部分。

下面是 Windows 7 计算机上的 **！ verifier** 扩展的示例。

```dbgcmd
2: kd> !verifier 0xf

Verify Level 9bb ... enabled options are:
    Special pool
    Special irql
    All pool allocations checked on unload
    Io subsystem checking enabled
    Deadlock detection enabled
    DMA checking enabled
    Security checks enabled
    Miscellaneous checks enabled

Summary of All Verifier Statistics

RaiseIrqls                             0x0
AcquireSpinLocks                       0x362
Synch Executions                       0x0
Trims                                  0xa34a

Pool Allocations Attempted             0x7b058
Pool Allocations Succeeded             0x7b058
Pool Allocations Succeeded SpecialPool 0x7b058
Pool Allocations With NO TAG           0x0
Pool Allocations Failed                0x0
Resource Allocations Failed Deliberately   0x0

Current paged pool allocations         0x1a for 00000950 bytes
Peak paged pool allocations            0x1b for 00000AC4 bytes
Current nonpaged pool allocations      0xe3 for 00046110 bytes
Peak nonpaged pool allocations         0x10f for 00048E40 bytes

Driver Verification List

Entry     State           NonPagedPool   PagedPool   Module

fffffa8003b6f670 Loaded           000000a0       00000854    videoprt.sys

Current Pool Allocations  00000002    00000013
Current Pool Bytes        000000a0    00000854
Peak Pool Allocations     00000006    00000014
Peak Pool Bytes           000008c0    000009c8

PoolAddress  SizeInBytes    Tag       CallersAddress
fffff9800157efc0     0x0000003c     Vprt      fffff88002c62963
fffff9800146afc0     0x00000034     Vprt      fffff88002c62963
fffff980015bafe0     0x00000018     Vprt      fffff88002c628f7
...

fffffa8003b6f620 Loaded           00046070       000000fc    usbport.sys

Current Pool Allocations  000000e1    00000007
Current Pool Bytes        00046070    000000fc
Peak Pool Allocations     0000010d    0000000a
Peak Pool Bytes           00048da0    00000254

PoolAddress  SizeInBytes    Tag       CallersAddress
fffff98003a38fc0     0x00000038     usbp      fffff88004215e34
fffff98003a2cfc0     0x00000038     usbp      fffff88004215e34
fffff9800415efc0     0x00000038     usbp      fffff88004215e34
...

----------------------------------------------- 
Fault injection trace log                       
----------------------------------------------- 

Driver Verifier didn't inject any faults.

----------------------------------------------- 
Track irql trace log                            
----------------------------------------------- 

Displaying most recent 0x0000000000000004 entries from the IRQL transition log.
There are up to 0x100 entries in the log.

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff8800420f2ca USBPORT!USBPORT_DM_IoTimerDpc+0x9a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66
    fffff80002a7bdd6 nt!KiProcessExpiredTimerList+0xc6
    fffff80002a7c4be nt!KiTimerExpiration+0x1be

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff88004205f3a USBPORT!USBPORT_AcquireEpListLock+0x2e
    fffff880042172df USBPORT!USBPORT_Core_TimeoutAllTransfers+0x1f
    fffff8800420f2ca USBPORT!USBPORT_DM_IoTimerDpc+0x9a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff88004201694 USBPORT!MPf_CheckController+0x4c
    fffff8800420f26a USBPORT!USBPORT_DM_IoTimerDpc+0x3a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66
    fffff80002a7bdd6 nt!KiProcessExpiredTimerList+0xc6

Thread:             fffff80002bf8c40
Old irql:           0000000000000002
New irql:           0000000000000002
Processor:          0000000000000000
Time stamp:         000000000000495e

    fffff8800420167c USBPORT!MPf_CheckController+0x34
    fffff8800420f26a USBPORT!USBPORT_DM_IoTimerDpc+0x3a
    fffff80002a5b5bf nt!IopTimerDispatch+0x132
    fffff80002a7c29e nt!KiProcessTimerDpcTable+0x66
    fffff80002a7bdd6 nt!KiProcessExpiredTimerList+0xc6
```

下面是启用了第7位并指定了 *地址* 的 Windows Vista 计算机上的 **！ verifier** 扩展的示例。

```dbgcmd
0: kd> !verifier 80 a2b1cf20
# Parsing 00004000 array entries, searching for address a2b1cf20.

Pool block a2b1ce98, Size 00000168, Thread a2b1ce98
808f1be6 ndis!ndisFreeToNPagedPool+0x39
808f11c1 ndis!ndisPplFree+0x47
808f100f ndis!NdisFreeNetBufferList+0x3b
8088db41 NETIO!NetioFreeNetBufferAndNetBufferList+0xe
8c588d68 tcpip!UdpEndSendMessages+0xdf
8c588cb5 tcpip!UdpSendMessagesDatagramsComplete+0x22
8088d622 NETIO!NetioDereferenceNetBufferListChain+0xcf
8c5954ea tcpip!FlSendNetBufferListChainComplete+0x1c
809b2370 ndis!ndisMSendCompleteNetBufferListsInternal+0x67
808f1781 ndis!NdisFSendNetBufferListsComplete+0x1a
8c04c68e pacer!PcFilterSendNetBufferListsComplete+0xb2
809b230c ndis!NdisMSendNetBufferListsComplete+0x70
# 8ac4a8ba test1!HandleCompletedTxPacket+0xea

Pool block a2b1ce98, Size 00000164, Thread a2b1ce98
822af87f nt!VerifierExAllocatePoolWithTagPriority+0x5d
808f1c88 ndis!ndisAllocateFromNPagedPool+0x1d
808f11f3 ndis!ndisPplAllocate+0x60
808f1257 ndis!NdisAllocateNetBufferList+0x26
80890933 NETIO!NetioAllocateAndReferenceNetBufferListNetBufferMdlAndData+0x14
8c5889c2 tcpip!UdpSendMessages+0x503
8c05c565 afd!AfdTLSendMessages+0x27
8c07a087 afd!AfdTLFastDgramSend+0x7d
8c079f82 afd!AfdFastDatagramSend+0x5ae
8c06f3ea afd!AfdFastIoDeviceControl+0x3c1
8217474f nt!IopXxxControlFile+0x268
821797a1 nt!NtDeviceIoControlFile+0x2a
8204d16a nt!KiFastCallEntry+0x127
```

 

