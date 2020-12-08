---
title: 解释 Bug 检查 0xCB
description: 解释 Bug 检查 0xCB
keywords:
- 内核流调试，视频流延迟，bug 检查0xcb
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d402d67d363cf4689bc2e4fb5c11f212c13710e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838177"
---
# <a name="interpreting-bug-check-0xcb"></a>解释 Bug 检查 0xCB


与调试视频流延迟关联的最常见 bug 检查代码为 Bug 检查 0xCB (驱动程序 \_ 已 \_ \_ \_ 在进程) 中保留锁定页面 \_ 。 有关参数的详细列表，请参阅 [**Bug 检查 0xCB**](bug-check-0xcb--driver-left-locked-pages-in-process.md)。

Bug 检查发生时所显示的消息将作为原因指向 Ks.sys。

```dbgcmd
Use !analyze -v to get detailed debugging information.
BugCheck CB, {f90c6ae0, f9949215, 81861788, 26}
Probably caused by : ks.sys ( ks!KsProbeStreamIrp+333 )
```

如建议，请使用 [**！分析-v**](-analyze.md) 以获取更多详细信息。

```dbgcmd
kd> !analyze -v
DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS (cb)
Caused by a driver not cleaning up completely after an I/O.
When possible, the guilty driver's name (Unicode string) is printed on
the bugcheck screen and saved in KiBugCheckDriver.
Arguments:
Arg3: 81861788, A pointer to the MDL containing the locked pages.
```

现在，使用 [**！搜索**](-search.md) 扩展查找与 MDL 指针关联的虚拟地址。

```dbgcmd
kd> !search 81861788
Searching PFNs in range 00000001 - 0000FF76 for [FFFFFFFF81861788 - FFFFFFFF81861788]

Pfn      Offset   Hit      Va       Pte
- - - - - - - - - - - - - - - - - - - - - - - - - - -
000008A7 00000B0C 81861788 808A7B0C C020229C
00000A04 00000224 16000001 80A04224 C0202810
...
00001732 000009B4 81861788 817329B4 C0205CC8
```

对于每个虚拟地址 (VA) 找到，请查找 IRP 签名。 为此，请使用带有 VA 减一个 DWORD 的 [**dd**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 命令。

```dbgcmd
kd> dd 808A7B0C-4 l4
808a7b08  f9949215 81861788 00000026 00000000
kd> $ Not an Irp
kd> dd 80A04224-4 l4
80a04220  00000000 00000000 00000000 00000000
kd> $ Not an Irp
kd> dd 817329B4-4 l4
817329b0  01900006 81861788 00000070 ffa59220
kd> $ Matches signature
```

找到具有 IRP 签名的 VA 后，请使用 [**！ IRP**](-irp.md) 扩展来找出正在此 IRP 上挂起的驱动程序。

```dbgcmd
kd> !irp 817329b0 7
Irp is active with 2 stacks 2 is current (= 0x81732a44)
 Mdl = 81861788 System buffer = ffa59220 Thread 00000000:  Irp stack trace.
>[  e, 0]   1  1 81a883c8 81ae6158 00000000-00000000    pending
 \Driver\TESTCAP
                        Args: 00000070 00000000 002f4017 00000000
```

在这种情况下， \\ 驱动程序 \\ TESTCAP 是错误检查的可能原因。

 

 





