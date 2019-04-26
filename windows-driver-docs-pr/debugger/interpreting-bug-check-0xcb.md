---
title: 解释 Bug 检查 0xCB
description: 解释 Bug 检查 0xCB
ms.assetid: 82951e2b-cbb2-45d2-a6b8-4fddece035ce
keywords:
- 内核调试，流式处理视频流停滞 bug 检查 0xcb
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eed9d18e7fe58a525f8f48af33990c6a23f30b28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327339"
---
# <a name="interpreting-bug-check-0xcb"></a>解释 Bug 检查 0xCB


与调试视频流停止关联的最常见 bug 检查代码是 Bug 检查 0xCB (驱动程序\_左侧\_已锁定\_页面\_IN\_过程)。 其参数的详细列表，请参阅[ **Bug 检查 0xCB**](bug-check-0xcb--driver-left-locked-pages-in-process.md)。

检查错误发生时所显示的消息将指向 Ks.sys 寻找原因。

```dbgcmd
Use !analyze -v to get detailed debugging information.
BugCheck CB, {f90c6ae0, f9949215, 81861788, 26}
Probably caused by : ks.sys ( ks!KsProbeStreamIrp+333 )
```

作为建议，使用[ **！ 分析-v** ](-analyze.md)以获取更多详细的信息。

```dbgcmd
kd> !analyze -v
DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS (cb)
Caused by a driver not cleaning up completely after an I/O.
When possible, the guilty driver's name (Unicode string) is printed on
the bugcheck screen and saved in KiBugCheckDriver.
Arguments:
Arg3: 81861788, A pointer to the MDL containing the locked pages.
```

现在，使用[ **！ 搜索**](-search.md)扩展查找与 MDL 指针相关联的虚拟地址。

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

找到每个虚拟地址 (VA)，查找 IRP 签名。 执行此操作通过使用[ **dd** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令和减去一个 DWORD VA。

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

找到具有 IRP 签名 VA 后，使用[ **！ irp** ](-irp.md)扩展以找出哪些驱动程序为挂起此 IRP 上。

```dbgcmd
kd> !irp 817329b0 7
Irp is active with 2 stacks 2 is current (= 0x81732a44)
 Mdl = 81861788 System buffer = ffa59220 Thread 00000000:  Irp stack trace.
>[  e, 0]   1  1 81a883c8 81ae6158 00000000-00000000    pending
 \Driver\TESTCAP
                        Args: 00000070 00000000 002f4017 00000000
```

在这种情况下，\\驱动程序\\TESTCAP 是可能的原因的错误检查。

 

 





