---
title: 实时本地调试
description: 实时本地调试
keywords:
- 内核流调试，实时本地调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd27efb2bd964a1889c6f8f5efc086291ddf2730
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806505"
---
# <a name="live-local-debugging"></a>实时本地调试


在 Microsoft Windows XP 和更高版本的操作系统中，可以通过使用 **-kl** 命令行选项启动内核调试器 (KD) 或 WinDbg 来执行本地内核调试：

```console
kd [-y SymbolPath] -kl 
```

或

```console
windbg [-y SymbolPath] -kl 
```

在 Windows Vista 和更高版本中，本地内核调试需要计算机通过 **/debug** 选项来启动。 以管理员身份打开命令提示符窗口，然后 **在上输入 bcdedit/debug**。 重新启动计算机。

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

在 Windows Vista 和更高版本中，本地内核调试需要以管理员身份运行调试器。

实时本地调试非常适合用于调试在附加调试器时难以重现的问题;但是，除非问题是挂起或延迟，否则需要知道时间敏感信息的任何内容（包括数据包、IRP 和 SRB 数据）都不可能工作。

执行本地调试时，请考虑以下变量：

-   **总体状态。** 例如，流是否正在运行？ 流是否已暂停？

-   **数据包计数。** 例如，是否有作业排队等候流？

-   **数据包计数的变化。** 流是否正在移动？

-   **数据包列表中的更改。**

-   **挂起内核线程。**

请考虑其中的最后一个。

### <a name="span-idexamining_a_hung_thread_in_lkdspanspan-idexamining_a_hung_thread_in_lkdspanexamining-a-hung-thread-in-lkd"></a><span id="examining_a_hung_thread_in_lkd"></span><span id="EXAMINING_A_HUNG_THREAD_IN_LKD"></span>检查 LKD 中的挂起线程

首先，使用 [**！ process 0 0**](-process.md) 扩展来标识包含挂起线程的进程。 然后，再次出现！有关该线程的详细信息，请再次 **处理** 此问题：

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

线程未显示，但堆栈地址为。 在堆栈上的当前地址上使用 [**dds**](dds--dps--dqs--display-words-and-symbols-.md) (或 **ddq**) 命令将产生一个开始点，以便进一步调查，因为它指定了正在调用哪个进程。

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

 

 





