---
title: AML 调试示例
description: AML 调试示例
keywords:
- AMLI 调试器，调试示例
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 65dbfbbc0576849b554b429381847d81c60c0876
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783571"
---
# <a name="aml-debugging-examples"></a>AML 调试示例


## <span id="ddk_aml_debugging_examples_dbg"></span><span id="DDK_AML_DEBUGGING_EXAMPLES_DBG"></span>


下面是演示如何开始 AML 调试的示例。

### <a name="span-idinvestigating_a_frozen_computerspanspan-idinvestigating_a_frozen_computerspaninvestigating-a-frozen-computer"></a><span id="investigating_a_frozen_computer"></span><span id="INVESTIGATING_A_FROZEN_COMPUTER"></span>调查冻结计算机

如果目标计算机已冻结，但您怀疑这可能是一个 ACPI 问题，请首先使用 [**！ amli lc**](-amli-lc.md) 扩展显示所有活动上下文：

```dbgcmd
kd> !amli lc
*Ctxt=ffffffff8128d000, ThID=ffffffff81277880, Flgs=----R----, pbOp=ffffffff8124206c, Obj=\_SB.PCI0.ISA0.FDC0._CRS
```

如果未显示上下文，则该错误可能不是 ACPI 相关的。

如果显示了上下文，请查找用星号标记的上下文。 这是 *当前上下文* (在当前时刻由解释器执行的上下文) 。

在此示例中，目标计算机在32位处理器上运行 Windows。 因此，所有地址都强制转换为64位，从而产生了高32位的免费 FFFFFFFF。 缩写 **pbOp** 指示指令指针 ( "指向二进制操作代码的指针" ) 。 **Obj** 字段提供了方法在 ACPI 表中的完整路径和名称。 有关标志的说明，请参阅 [**！ amli lc**](-amli-lc.md)。

可以使用 [**！ amli u**](-amli-u.md) 命令来拆装 \_ CRS 方法，如下所示：

```dbgcmd
kd> !amli u \_SB.PCI0.ISA0.FDC0._CRS

ffffffff80e4a535 : CreateDWordFieldCRES, 0x76, RAMT)
ffffffff80e4a540 : CreateDWordField(CRES, 0x82, PCIT)
ffffffff80e4a54b : Add(MLEN(), 0x100000, RAMT)
ffffffff80e4a559 : Subtract(0xffe00000, RAMT, PCIT)
ffffffff80e4a567 : Return(CRES)
```

### <a name="span-idbreaking_into_the_amli_debuggerspanspan-idbreaking_into_the_amli_debuggerspanbreaking-into-the-amli-debugger"></a><span id="breaking_into_the_amli_debugger"></span><span id="BREAKING_INTO_THE_AMLI_DEBUGGER"></span>中断 AMLI 调试器

[**！ Amli 调试器**](-amli-debugger.md)命令使 aml 解释器在下一次执行任何 AML 代码时中断到 amli 调试器。

显示 AMLI 调试器提示后，可以使用任何 AMLI 调试器命令。 你还可以使用 **！ amli** extension 命令，而无需使用 "！ amli" 作为前缀：

```dbgcmd
kd> !amli debugger
kd> g

AMLI(? for help)-> find _crs
\_SB.LNKA._CRS
\_SB.LNKB._CRS
\_SB.LNKC._CRS
\_SB.LNKD._CRS
\_SB.PCI0._CRS
\_SB.PCI0.LPC.NCP._CRS
\_SB.PCI0.LPC.PIC._CRS
\_SB.PCI0.LPC.TIME._CRS
\_SB.PCI0.LPC.IDMA._CRS
\_SB.PCI0.LPC.RTC._CRS
\_SB.PCI0.LPC.SPKR._CRS
\_SB.PCI0.LPC.FHUB._CRS
\_SB.PCI0.SBD1._CRS
\_SB.PCI0.SBD2._CRS
\_SB.MBRD._CRS

AMLI(? for help)-> u \_SB.PCI0._CRS

ffffffff80e4a535 : CreateDWordFieldCRES, 0x76, RAMT)
ffffffff80e4a540 : CreateDWordField(CRES, 0x82, PCIT)
ffffffff80e4a54b : Add(MLEN(), 0x100000, RAMT)
ffffffff80e4a559 : Subtract(0xffe00000, RAMT, PCIT)
ffffffff80e4a567 : Return(CRES)
```

### <a name="span-idusing_breakpointsspanspan-idusing_breakpointsspanusing-breakpoints"></a><span id="using_breakpoints"></span><span id="USING_BREAKPOINTS"></span>使用断点

在下面的示例中，将在执行方法 BST 之前中断 AMLI 调试器 \_ 。

即使您找到了 \_ BST 对象，也应该验证它确实是一种方法。 可以使用 [**！ amli dns**](-amli-dns.md) 扩展来执行此操作。

```dbgcmd
kd> !amli dns /s \_sb.pci0.isa.bat1._bst

ACPI Name Space: \_SB.PCI0.ISA.BAT1._BST (c29c2044)
Method(_BST:Flags=0x0,CodeBuff=c29c20a5,Len=103)
```

现在，可以使用 [**！ amli bp**](-amli-bp.md) 命令放置断点：

```dbgcmd
kd> !amli bp \_sb.pci0.isa.bat1._bst
```

你可能还需要在方法中放置断点。 可以使用 [**！ amli u**](-amli-u.md) 命令来反汇编 \_ BST，然后在其中一个步骤中放置断点：

```dbgcmd
kd> !amli u _sb.pci0.isa.bat1._bst

ffffffffc29c20a5: Acquire(\_SB_.PCI0.ISA_.EC0_.MUT1, 0xffff)
ffffffffc29c20c0: Store("CMBatt - _BST.BAT1", Debug)
ffffffffc29c20d7: \_SB_.PCI0.ISA_.EC0_.CPOL()
ffffffffc29c20ee: Release(\_SB_.PCI0.ISA_.EC0_.MUT1)
ffffffffc29c2107: Return(PBST)

kd> !amli bp c29c20ee
```

### <a name="span-idresponding_to_a_triggered_breakpointspanspan-idresponding_to_a_triggered_breakpointspanresponding-to-a-triggered-breakpoint"></a><span id="responding_to_a_triggered_breakpoint"></span><span id="RESPONDING_TO_A_TRIGGERED_BREAKPOINT"></span>响应触发的断点

在下面的示例中，方法 \_ WAK 正在运行，然后遇到断点：

```dbgcmd
Running \_WAK method
Hit Breakpoint 0.
```

使用 [**！ amli ln**](-amli-ln.md) 扩展查看当前程序计数器的最近方法。 下面的示例显示了32位格式的地址：

```dbgcmd
kd> !amli ln
c29accf5: \_WAK
```

[**！ Amli lc**](-amli-lc.md)扩展显示所有活动上下文：

```dbgcmd
kd> !amli lc
 Ctxt=c18b6000, ThID=00000000, Flgs=A-QC-W----, pbOp=c29bf8fe, Obj=\_SB.PCI0.ISA.EC0._Q09
*Ctxt=c18b4000, ThID=c15a6618, Flgs=----R-----, pbOp=c29accf5, Obj=\_WAK
```

这表明活动上下文与 Q09-ft-sye 和 WAK 方法相关联 \_ \_ 。 当前上下文为 \_ WAK。

现在，可以使用 [**！ amli r**](-amli-r.md) 命令显示有关当前上下文的更多详细信息。 从此，可以看到有用的线程和堆栈信息，以及传递到 \_ WAK 和本地数据对象的参数。

```dbgcmd
kd> !amli r
Context=c18b4000*, Queue=00000000, ResList=00000000
ThreadID=c15a6618, Flags=00000010
StackTop=c18b5eec, UsedStackSize=276 bytes, FreeStackSize=7636 bytes
LocalHeap=c18b40c0, CurrentHeap=c18b40c0, UsedHeapSize=88 bytes
Object=\_WAK, Scope=\_WAK, ObjectOwner=c18b4108, SyncLevel=0
AsyncCallBack=ff06b5d0, CallBackData=0, CallBackContext=c99efddc

MethodObject=\_WAK
c18b40e4: Arg0=Integer(:Value=0x00000001[1])
c18b5f3c: Local0=Unknown()
c18b5f54: Local1=Unknown()
c18b5f6c: Local2=Unknown()
c18b5f84: Local3=Unknown()
c18b5f9c: Local4=Unknown()
c18b5fb4: Local5=Unknown()
c18b5fcc: Local6=Unknown()
c18b5fe4: Local7=Unknown()
c18b4040: RetObj=Unknown()
```

### <a name="span-idtracing__stepping__and_running_aml_codespanspan-idtracing__stepping__and_running_aml_codespantracing-stepping-and-running-aml-code"></a><span id="tracing__stepping__and_running_aml_code"></span><span id="TRACING__STEPPING__AND_RUNNING_AML_CODE"></span>跟踪、单步执行和运行 AML 代码

如果要跟踪代码，可以使用 [**！ amli set**](-amli-set.md) extension 来打开完整的跟踪信息，如下所示：

```dbgcmd
kd> !amli set spewon verboseon traceon
```

现在，您可以单步执行 AML 代码，并逐行执行代码。 **P** 命令执行任何函数调用的步骤。 **T** 命令将单步执行函数调用。

```dbgcmd
AMLI(? for help)-> p

c29bfcb7: Store(\_SB_.PCI0.ISA_.ACAD.CHAC(SEL0=0x10e1)
c29c17b1: {
c29c17b1: | Store(LGreater(And(Arg0=0x10e1,0xf0,)=0xe0,0x80)=0xffffffff,Local0)=0xffffffff

AMLI(? for help)-> p

c29c17bb: | If(LNot(LEqual(Local0=0xffffffff,ACP_=0xffffffff)=0xffffffff)=0x0)
c29c17ce: | {
c29c17ce: | | Return(Zero)
c29c17d0: | }
c29c17d0: },Local1)=0x0

AMLI(? for help)-> t

c29bfcd4: Store(\_SB_.PCI0.ISA_.BAT1.CHBP(SEL0=0x10e1)
c29c293d: {
c29c293d: | Store("CMBatt - CHBP.BAT1",Debug)String(:Str="CMBatt - CHBP.BAT1")="CMBatt - CHBP.BAT1"
```

你还可以在 AMLI 调试器中运行方法（如果你选择）。 例如，你可以通过运行其控制方法 STA 来评估 LNKA 设备的状态 \_ ：

```dbgcmd
AMLI(? for help)-> run \_sb.lnka._sta
PCI OpRegion Access on region c29b2268 device c29b2120

\_SB.LNKA._STA completed successfully with object data:
Integer(:Value=0x0000000b[11])
```

## <a name="see-also"></a>另请参阅

 [AMLI 调试器](the-amli-debugger.md)

 





