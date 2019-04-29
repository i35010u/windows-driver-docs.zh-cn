---
title: AML 调试示例
description: AML 调试示例
ms.assetid: 3a9f760f-f511-412f-aca0-3c415b3e5dc2
keywords:
- AMLI 调试器，调试示例
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e090547a65b599eb1f778d7a012f17a0b8ffd853
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355006"
---
# <a name="aml-debugging-examples"></a>AML 调试示例


## <span id="ddk_aml_debugging_examples_dbg"></span><span id="DDK_AML_DEBUGGING_EXAMPLES_DBG"></span>


下面是示例，展示了如何开始使用 AML 调试。

### <a name="span-idinvestigatingafrozencomputerspanspan-idinvestigatingafrozencomputerspaninvestigating-a-frozen-computer"></a><span id="investigating_a_frozen_computer"></span><span id="INVESTIGATING_A_FROZEN_COMPUTER"></span>调查已冻结的计算机

如果目标计算机已冻结，并且怀疑它可能是 ACPI 问题，应首先使用[ **！ amli lc** ](-amli-lc.md)扩展以显示所有活动的上下文：

```dbgcmd
kd> !amli lc
*Ctxt=ffffffff8128d000, ThID=ffffffff81277880, Flgs=----R----, pbOp=ffffffff8124206c, Obj=\_SB.PCI0.ISA0.FDC0._CRS
```

如果未不显示任何上下文，错误可能不是 ACPI 相关。

如果上下文所示，寻找标有星号的一个。 这是*当前上下文*（正在执行的解释器目前存在一个）。

在此示例中，目标计算机运行 Windows 32 位处理器上。 因此所有地址都强制都转换为 64 位，生成的高 32 位中剔除 FFFFFFFF。 缩写**pbOp**指示指令指针 （"指向二元运算符代码"）。 **Obj**字段提供的完整路径和方法的名称显示在 ACPI 表中。 有关的标志的说明，请参阅[ **！ amli lc**](-amli-lc.md)。

可以使用[ **！ amli u** ](-amli-u.md)命令反汇编\_CRS 方法，如下所示：

```dbgcmd
kd> !amli u \_SB.PCI0.ISA0.FDC0._CRS

ffffffff80e4a535 : CreateDWordFieldCRES, 0x76, RAMT)
ffffffff80e4a540 : CreateDWordField(CRES, 0x82, PCIT)
ffffffff80e4a54b : Add(MLEN(), 0x100000, RAMT)
ffffffff80e4a559 : Subtract(0xffe00000, RAMT, PCIT)
ffffffff80e4a567 : Return(CRES)
```

### <a name="span-idbreakingintotheamlidebuggerspanspan-idbreakingintotheamlidebuggerspanbreaking-into-the-amli-debugger"></a><span id="breaking_into_the_amli_debugger"></span><span id="BREAKING_INTO_THE_AMLI_DEBUGGER"></span>中断到 AMLI 调试器

[ **！ Amli 调试器**](-amli-debugger.md)命令将导致 AML 解释器在中断 AMLI 调试器在下次执行任何 AML 代码。

AMLI 调试器后会出现提示，您可以使用任何 AMLI 调试器命令。 此外可以使用 **！ amli**扩展命令不使用前缀"！ amli":

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

### <a name="span-idusingbreakpointsspanspan-idusingbreakpointsspanusing-breakpoints"></a><span id="using_breakpoints"></span><span id="USING_BREAKPOINTS"></span>使用断点

在以下示例中，将进入该方法之前 AMLI 调试器\_BST 执行。

即使您位于\_BST 对象时，应验证它确实是一个方法。 可以使用[ **！ amli dns** ](-amli-dns.md)扩展来执行此操作。

```dbgcmd
kd> !amli dns /s \_sb.pci0.isa.bat1._bst

ACPI Name Space: \_SB.PCI0.ISA.BAT1._BST (c29c2044)
Method(_BST:Flags=0x0,CodeBuff=c29c20a5,Len=103)
```

现在，可以使用[ **！ amli bp** ](-amli-bp.md)放置断点的命令：

```dbgcmd
kd> !amli bp \_sb.pci0.isa.bat1._bst
```

您可能想要放置在方法中的断点。 可以使用[ **！ amli u** ](-amli-u.md)命令反汇编\_BST，然后将断点放在其步骤之一：

```dbgcmd
kd> !amli u _sb.pci0.isa.bat1._bst

ffffffffc29c20a5: Acquire(\_SB_.PCI0.ISA_.EC0_.MUT1, 0xffff)
ffffffffc29c20c0: Store("CMBatt - _BST.BAT1", Debug)
ffffffffc29c20d7: \_SB_.PCI0.ISA_.EC0_.CPOL()
ffffffffc29c20ee: Release(\_SB_.PCI0.ISA_.EC0_.MUT1)
ffffffffc29c2107: Return(PBST)

kd> !amli bp c29c20ee
```

### <a name="span-idrespondingtoatriggeredbreakpointspanspan-idrespondingtoatriggeredbreakpointspanresponding-to-a-triggered-breakpoint"></a><span id="responding_to_a_triggered_breakpoint"></span><span id="RESPONDING_TO_A_TRIGGERED_BREAKPOINT"></span>响应触发断点

在下面的示例中，该方法\_WAK 正在运行，并且然后遇到断点：

```dbgcmd
Running \_WAK method
Hit Breakpoint 0.
```

使用[ **！ amli ln** ](-amli-ln.md)扩展以查看当前的程序计数器最近的方法。 下面的示例在 32 位窗体中显示地址：

```dbgcmd
kd> !amli ln
c29accf5: \_WAK
```

[ **！ Amli lc** ](-amli-lc.md)扩展插件都会显示所有活动的上下文：

```dbgcmd
kd> !amli lc
 Ctxt=c18b6000, ThID=00000000, Flgs=A-QC-W----, pbOp=c29bf8fe, Obj=\_SB.PCI0.ISA.EC0._Q09
*Ctxt=c18b4000, ThID=c15a6618, Flgs=----R-----, pbOp=c29accf5, Obj=\_WAK
```

这将显示活动的上下文相关联的方法\_Q09 和\_WAK。 当前上下文是\_WAK。

现在，可以使用[ **！ amli r** ](-amli-r.md)命令以显示有关当前上下文的更多详细信息。 可以从此看到线程和堆栈的有用信息，以及自变量传递给\_WAK 和本地数据对象。

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

### <a name="span-idtracingsteppingandrunningamlcodespanspan-idtracingsteppingandrunningamlcodespantracing-stepping-and-running-aml-code"></a><span id="tracing__stepping__and_running_aml_code"></span><span id="TRACING__STEPPING__AND_RUNNING_AML_CODE"></span>跟踪、 单步执行，以及运行 AML 代码

如果你要跟踪通过代码，您可以使用来启用完整的跟踪信息[ **！ amli 集**](-amli-set.md)扩展，如下所示：

```dbgcmd
kd> !amli set spewon verboseon traceon
```

现在逐句通过 AML 代码，并监视执行的行的行的代码。 **P**通过任何函数调用命令的步骤。 **T**命令将单步执行函数调用。

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

如果愿意，还可能会运行从 AMLI 调试器中的方法。 例如，可能通过运行其控件方法评估 LNKA 设备的状态\_STA:

```dbgcmd
AMLI(? for help)-> run \_sb.lnka._sta
PCI OpRegion Access on region c29b2268 device c29b2120

\_SB.LNKA._STA completed successfully with object data:
Integer(:Value=0x0000000b[11])
```

## <a name="see-also"></a>请参阅

 [AMLI 调试器](the-amli-debugger.md)

 





