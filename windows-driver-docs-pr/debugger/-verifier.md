---
title: verifier
description: 验证程序扩展显示驱动程序验证程序和其操作的状态。
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
ms.openlocfilehash: 2b6d34dc523b2e22ba854f1d4ade395862c60b29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362417"
---
# <a name="verifier"></a>!verifier


**！ Verifier**扩展显示驱动程序验证程序和其操作的状态。

驱动程序验证程序包含在 Windows 中。 它适用于已检查和免费版本。 有关驱动程序验证程序的信息，请参阅[Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480) Windows Driver Kit (WDK) 文档中的主题。

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

## <a name="span-idddkverifierdbgspanspan-idddkverifierdbgspanparameters"></a><span id="ddk__verifier_dbg"></span><span id="DDK__VERIFIER_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定此命令的输出中显示的信息。 如果*标志*是等于的值 4、 8、 0x20、 0x40、 0x80，或 0x100，然后为其余参数 **！ verifier**基于这些值与关联的特定参数进行解释。 如果*标志*等同于任何其他值，即使一个或多个这些位将设置，仅*标志*并*图像*允许参数。 *标志*可以是以下位的任何总和; 默认值为 0:

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
显示正在验证的所有驱动程序的名称。 此外会显示从非分页缓冲的池和页面缓冲的池当前分配给每个驱动程序的字节数。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
显示池 （池大小、 标头和池标记） 和未完成的内存分配保留的卸载驱动程序有关的信息。 除非还设置位 0 (0x1)，则此标志无效。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
显示错误注入的信息。 显示的寄信人地址、 符号名称和请求每个分配的代码的偏移量。 如果*标志*是完全 0x4 和*Quantity*包含参数的值，可以选择显示这些记录数。 否则，将显示四个记录。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示正在验证的驱动程序所做的最新的 IRQL 更改。 显示旧的 IRQL、 新的 IRQL、 处理器和时间戳。 如果*标志*是完全 0x8 并且*Quantity*包含参数的值，可以选择显示这些记录数。 否则，将显示四个记录。

**警告**  在 64 位版本的 Windows，一些提高或降低 IRQL 的内核函数实现为内联代码而不是导出的函数。 驱动程序验证程序执行操作所做的内联代码，因此可以由驱动程序验证程序不完整的 IRQL 转换日志的未报告的 IRQL 更改。 请参阅备注有关缺少的 IRQL 转换条目的示例。

 

<span id="Bit_6__0x40_"></span><span id="bit_6__0x40_"></span><span id="BIT_6__0X40_"></span>第 6 位 (0x40)  
(Windows Vista 及更高版本)显示的信息**强制挂起 I/O 请求**挂起的 Irp 强制驱动程序验证程序，包括从的日志中跟踪的选项。

*数量*参数指定要显示的跟踪号。 默认情况下，显示整个日志。

<span id="Bit_7__0x80_"></span><span id="bit_7__0x80_"></span><span id="BIT_7__0X80_"></span>7 位 (0x80)  
(Windows Vista 及更高版本)显示内核池分配/可用日志中的信息。

*数量*参数指定要显示的跟踪号。 默认情况下，显示整个日志。

如果*地址*指定，则会显示仅与内核池分配/可用日志中指定的地址相关联的跟踪。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>位 8 (0x100)  
(Windows Vista 及更高版本)显示日志中的 IoAllocateIrp、 IoCompleteRequest 和 IoCancelIrp 调用的信息。

数量参数指定要显示的跟踪号。 默认情况下，显示整个日志。

如果*地址*指定，则会显示仅与指定的 IRP 地址相关联的跟踪。

<span id="Bit_9__0x200_"></span><span id="bit_9__0x200_"></span><span id="BIT_9__0X200_"></span>9 (0x200) 位  
(Windows Vista 及更高版本)临界区日志中显示的条目。

如果*地址*指定，则将显示仅与指定的线程地址相关联的项。

<span id="Bit_10__0x400_"></span><span id="bit_10__0x400_"></span><span id="BIT_10__0X400_"></span>位 10 (0x400)  
(Windows Vista 及更高版本)显示已取消当前正在监视的驱动程序验证程序的 Irp。

如果*地址*指定，则会显示仅使用指定的地址 IRP。

<span id="Bit_11__0x800_"></span><span id="bit_11__0x800_"></span><span id="BIT_11__0X800_"></span>位 11 (0x800)  
(Windows 8.1 及更高版本)显示您选择时，会创建错误注入日志中的条目[系统资源不足模拟](https://docs.microsoft.com/windows-hardware/drivers/devtest/systematic-low-resource-simulation)选项。

<span id="_______Image______"></span><span id="_______image______"></span><span id="_______IMAGE______"></span> *图像*   
如果*标志*使用和不等于 4、 8 或 0x10*映像*指定驱动程序的名称。 *图像*用来筛选显示的信息*标志*0x1 和 0x2 的值： 认为只有指定的驱动程序。 此驱动程序必须当前验证。

<span id="_______Quantity______"></span><span id="_______quantity______"></span><span id="_______QUANTITY______"></span> *数量*   
如果*标志*0x4，完全相等*Quantity*指定要显示的错误注入记录数。 如果*标志*0x8、 完全相等*Quantity*指定要显示的 IRQL 日志条目的数目。 如果*标志*0x40，完全相等*Quantity*指定的日志中显示的跟踪数强制挂起 Irp。 如果标志为 0x80 完全相等，数量指定的数从内核池分配/可用日志中显示的跟踪。 如果标志为 0x100 完全相等，数量指定从 IoAllocateIrp、 IoCompleteRequest 和 IoCancelIrp 调用的日志中显示的跟踪的数。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span> **-disable**   
清除上调试目标的当前驱动程序验证程序设置。 这些设置的清除不会保留通过重新启动。 如果你需要禁用驱动程序验证程序设置已成功启动，请在 nt 设置断点 ！VerifierInitSystem 并用 **！ verifier-禁用**此时命令。

<span id="______________"></span> **?**    
在调试器命令窗口中显示此扩展的一些简要帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

璝惠[Driver Verifier](https://go.microsoft.com/fwlink/p/?linkid=120480)，请参阅 Windows Driver Kit (WDK) 文档。


<a name="remarks"></a>备注
-------

下面的示例说明了，在 64 位版本的 Windows，IRQL 转换日志并不总是完成。 所示的两个条目是日志中的处理器 2 次连续的条目。 第一个条目显示为 0 会从 2 IRQL。 第二个条目都会显示 IRQL 转从 2 到 2。 找不到有关如何 IRQL 了引发从 0 到 2 的信息。

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

在使用驱动程序验证程序来测试图形驱动程序，使用[ **！ gdikdx.verifier** ](-gdikdx-verifier.md)而不是扩展 **！ verifier**。

值 4、 8 和 0x20、 0x40、 0x80，和 0x100 是特殊值*标志*。 如果将使用这些值，特殊的自变量中列出**参数**可以使用部分，并显示将包含仅与该标志值关联的信息。

如果任何其他值*标志*使用，即使一个或多个这些位将设置，仅*标志*并*图像*允许参数。 在此情况下，所有其他信息显示，除了 **！ verifier**将显示处于活动状态，以及有关池分配、 IRQL 引发、 自旋锁和修整的统计信息的 Driver Verifier 选项。

如果*标志*等于 0x20，为指定的值*CompletionTime*， *CancelTime*，以及*ForceCancellation*驱动程序使用挂起驱动程序验证程序的验证的选项。 到下次启动，这些新值将立即生效并且上一次。 重新引导时，它们将恢复为其默认值。

此外，如果*标志*等于 0x20 （有或没有其他参数） 打印驱动程序的挂起验证日志。 有关解释日志的信息，请参阅 Windows Driver Kit (WDK) 文档中的 Driver Verifier 文档的驱动程序的挂起的验证部分。

下面是举例 **！ verifier**的 Windows 7 计算机上的扩展。

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

下面是示例 **！ verifier**开启的 7 位的 Windows Vista 计算机上的扩展和*地址*指定。

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

 

 





