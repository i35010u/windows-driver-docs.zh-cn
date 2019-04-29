---
title: 实时本地调试
description: 实时本地调试
ms.assetid: ec76a71e-f173-4b66-beaf-d57a1c991acd
keywords:
- 内核调试，流式传输实时本地调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d57332b86f9aef90fa20abf6ad82ab94baa132e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383462"
---
# <a name="live-local-debugging"></a>实时本地调试


在 Microsoft Windows XP 和更高版本操作系统中，则可以执行本地内核调试通过启动内核调试程序 (KD) 或的 WinDbg **-kl**命令行选项：

```console
kd [-y SymbolPath] -kl 
```

或

```console
windbg [-y SymbolPath] -kl 
```

在 Windows Vista 及更高版本，本地内核调试要求计算机与启动 **/debug**选项。 打开命令提示符窗口，以管理员身份，并输入**bcdedit /debug 上的**。 重新启动计算机。

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

在 Windows Vista 及更高版本，本地内核调试需要以管理员身份运行调试器。

实时本地调试是非常有用的调试难以重现时将调试器附加; 的问题但是，任何需要的时间敏感信息，包括数据包、 IRP 和 SRB 知识数据，并不能解决问题除非挂起或停滞。

在执行本地调试时，请考虑以下变量：

-   **总体状态。** 例如，运行该流？ 已暂停流？

-   **对数据包进行计数。** 例如，是否有 Irp 排队发送至流？

-   **数据包计数方面的更改。** 移动流？

-   **数据包列表中的更改。**

-   **挂起的内核的线程。**

请考虑的最后一项。

### <a name="span-idexaminingahungthreadinlkdspanspan-idexaminingahungthreadinlkdspanexamining-a-hung-thread-in-lkd"></a><span id="examining_a_hung_thread_in_lkd"></span><span id="EXAMINING_A_HUNG_THREAD_IN_LKD"></span>检查 LKD 中的挂起线程

首先，使用[ **！ process 0 0** ](-process.md)扩展来识别包含挂起的线程的进程。 然后，发出 **！ 过程**再次为有关该线程的详细信息：

```dbgcmd
lkd> !process 816a550 7
        THREAD 81705da8  Cid 0b5c.0b60  Teb: 7ffde000 Win32Thread: e1b2d890 WAIT: (Suspended)
        IRP List:
            816c9ad8: (0006,0190) Flags: 00000030  Mdl: 00000000
        Start Address kernel32!BaseProcessStartThunk (0x77e5c650)
        Win32 Start Address 0x0101c9be
        Stack Init f50bf000 Current f50bea74 Base f50bf000 Limit f50b9000 Call 0
        Priority 10 BasePriority 8 PriorityDecrement 0
```

线程不会显示，但堆栈地址。 使用[ **dds** ](dds--dps--dqs--display-words-and-symbols-.md) (或**ddq**) 命令在堆栈的当前地址会产生进一步调查的起点，因为它指定哪个进程正在调用。

```dbgcmd
lkd> dds f50bea74
f50bea74  f50bebc4
f50bea78  00000000
f50bea7c  80805795 nt!KiSwapContext+0x25
f50beab4  8080ece0 nt!KeWaitForSingleObject
f50beabc  f942afda ks!CKsQueue::CancelAllIrps+0x14
f50bead8  f94406c4 ks!CKsQueue::SetDeviceState+0x170
f50beb00  f943f6f1 ks!CKsPipeSection::DistributeDeviceStateChange+0x1d
f50beb24  f943fb1e ks!CKsPipeSection::SetDeviceState+0xb2
```

 

 





