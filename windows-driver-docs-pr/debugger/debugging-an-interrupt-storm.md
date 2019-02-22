---
title: 调试中断 Storm
description: 调试中断 Storm
ms.assetid: b863cb9c-dce0-4572-b0ed-6f7d3a6ba472
keywords:
- 挂起的 Irp
- I/O 请求数据包 (IRP) 挂起
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d78ad3206adb2f283c924098b620ce818e19dc0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540662"
---
# <a name="debugging-an-interrupt-storm"></a>调试中断 Storm


## <span id="ddk_debugging_pending_irps_dbg"></span><span id="DDK_DEBUGGING_PENDING_IRPS_DBG"></span>


停止系统的最常见的示例之一是中断 storm。 *中断 storm*是保持断言状态级别触发中断信号。

以下事件可能会导致中断 storm:

-   硬件设备不会释放其中断信号后是定向的设备驱动程序。

-   设备驱动程序不会指示发布中断信号，其硬件，因为它不会检测中断已从其硬件启动。

-   设备驱动程序声明中断，即使不从其硬件初始化的中断也是如此。 多个设备都共享相同的 IRQ 时仅发生此情况。

-   边缘级别控制寄存器 (ELCR) 未正确设置。

-   边缘和级别触发中断的设备共享 IRQ （例如，COM 端口和 PCI SCSI 控制器）。

此示例演示一种方法可以检测和调试中断 storm。

机挂起，使用内核调试器中断。 使用 **！ irpfind**扩展命令要查找挂起的 Irp。 然后，使用 **！ irp**扩展能够获取有关任何挂起的 Irp 的详细信息。 例如：

```dbgcmd
kd> !irp 81183468 
Irp is active with 2 stacks 2 is current (= 0x811834fc)
 No Mdl Thread 00000000:  Irp stack trace.
     cmd  flg cl Device   File     Completion-Context
 [  0, 0]   0  0 8145f470 00000000 00000000-00000000
               \Driver\E100B
                        Args: 00000000 00000000 00000000 00000000
>[ 16, 2]   0 e1 8145f470 00000000 8047f744-814187a8 Success Error Cancel pending
               \Driver\E100B    ntoskrnl!PopCompleteSystemPowerIrp
                        Args: 00000000 00000000 00000002 00000002 
```

此示例演示\\驱动程序\\e100b 未返回有关 IRP **ntoskrnl ！PopCompleteSystemPowerIrp**。 它似乎会卡滞，可能会遇到中断 storm。

若要调查，请使用**kb**命令请求的堆栈跟踪。 例如：

```dbgcmd
kd> kb
ChildEBP RetAddr  Args to Child
f714ee68 8046355a 00000001 80068c10 00000030 ntoskrnl!RtlpBreakWithStatusInstruction
f714ee68 80067a4f 00000001 80068c10 00000030 ntoskrnl!KeUpdateSystemTime+0x13e
f714eeec 8046380b 01001010 0000003b f714ef00 halacpi!HalBeginSystemInterrupt+0x83
f714eeec 80463c50 01001010 0000003b f714ef00 ntoskrnl!KiChainedDispatch+0x1b
f714ef78 80067cc2 00000000 00000240 8000017c ntoskrnl!KiDispatchInterrupt
f714ef78 80501cb5 00000000 00000240 8000017c halacpi!HalpDispatchInterrupt2ndEnt  
```

请注意以粗体显示的部分是中断调度。 如果您使用**g**命令，并会破坏中同样，您将很有可能看到不同的堆栈跟踪，但仍会中断调度。 若要确定哪种中断负责系统停滞，请查看第二个参数传递到**HalBeginSystemInterrupt** （在此情况下，0x3B）。 标准规则是显示 (0x3B) 的中断向量是 IRQ 行加上 0x30，因此中断是数字 0xB。 运行另一个堆栈跟踪可能提供有关颁发中断服务请求 (ISR) 的设备的详细信息。 在这种情况下，第二个堆栈跟踪具有以下结果：

```dbgcmd
kd> kb
ChildEBP RetAddr  Args to Child
f714ee24 8046355a 00000001 00000010 00000030 ntoskrnl!RtlpBreakWithStatusInstruction
f714ee24 bfe854b9 00000001 00000010 00000030 ntoskrnl!KeUpdateSystemTime+0x13e
f714eed8 f7051796 00000000 80463850 8143ec88 atimpab!AtiInterrupt+0x109
f714eee0 80463850 8143ec88 81444038 8046380b VIDEOPRT!pVideoPortInterrupt+0x16
f714eef8 80463818 00000202 0000003b 80450bb8 ntoskrnl!KiChainedDispatch2ndLvl+0x28
f714eef8 80463c50 00000202 0000003b 80450bb8 ntoskrnl!KiChainedDispatch+0x28
f714ef78 80067cc2 00000000 00000240 8000017c ntoskrnl!KiDispatchInterrupt
f714ef78 80501cb5 00000000 00000240 8000017c halacpi!HalpDispatchInterrupt2ndEntry+0x1b
f714f084 8045f744 f714f16c 00020019 f714f148 ntoskrnl!NtCreateKey+0x113
f714f084 8042e487 f714f16c 00020019 f714f148 ntoskrnl!KiSystemService+0xc4
f714f118 804ab556 f714f16c 00020019 f714f148 ntoskrnl!ZwCreateKey+0xb
f714f184 8041f75b f714f1e8 8000017c f714f1d0 ntoskrnl!IopCreateRegistryKeyEx+0x4e
f714f204 804965cd 8145f630 00000000 00000001 ntoskrnl!IopProcessSetInterfaceState+0x93
f714f220 bfee1eb9 8145f630 00000000 8145f5a0 ntoskrnl!IoSetDeviceInterfaceState+0x2b
f714f254 bfedb416 00000004 00000800 0045f570 NDIS!ndisMCommonHaltMiniport+0x1f
f714f268 bfed4ddb bfed0660 811a2708 811a2708 NDIS!ndisPmHaltMiniport+0x9a
f714f288 bfed5146 811a2708 00000004 8145f570 NDIS!ndisSetPower+0x1d1
f714f2a8 8041c60f 81453a30 811a2708 80475b18 NDIS!ndisPowerDispatch+0x84
f714f2bc 8044cc52 80475b18 811a2708 811a279c ntoskrnl!IopfCallDriver+0x35
f714f2d4 8044cb89 811a279c 811a2708 811a27c0 ntoskrnl!PopPresentIrp+0x62 
```

系统当前正在运行视频卡的 ISR。 系统将为每个设备共享 IRQ 0xB 运行 ISR。 如果没有进程声称中断，操作系统将请求驱动程序来处理中断的 Isr 无限，等待。 还有可能，进程可能会处理中断和停止它，但如果硬件中断的中断可能只是重新断言。

使用 **！ 仲裁器 4**扩展来确定哪些设备位于 IRQ 0xB。 IRQ 0xB 时只有一个设备，如果您已经找到问题的原因... 如果有多个设备共享的中断 （99%的情况下)，将需要手动编程 LNK 节点 （这是对系统状态），或通过删除或禁用硬件隔离设备。

```dbgcmd
kd> !arbiter 4 
DEVNODE 8149a008 (HTREE\ROOT\0)
  Interrupt Arbiter "RootIRQ" at 80472a20
    Allocated ranges:
      0000000000000000 - 0000000000000000   B   8149acd0
      0000000000000001 - 0000000000000001   B   8149acd0
      0000000000000002 - 0000000000000002   B   8149acd0
      0000000000000003 - 0000000000000003   B   8149acd0
      0000000000000004 - 0000000000000004   B   8149acd0
      0000000000000005 - 0000000000000005   B   8149acd0
      0000000000000006 - 0000000000000006   B   8149acd0
      0000000000000007 - 0000000000000007   B   8149acd0
      0000000000000008 - 0000000000000008   B   8149acd0
      0000000000000009 - 0000000000000009   B   8149acd0
      000000000000000a - 000000000000000a   B   8149acd0
      000000000000000b - 000000000000000b   B   8149acd0
      000000000000000c - 000000000000000c   B   8149acd0
 000000000000000d - 000000000000000d   B   8149acd0
      000000000000000e - 000000000000000e   B   8149acd0
 000000000000000f - 000000000000000f   B   8149acd0
      0000000000000010 - 0000000000000010   B   8149acd0
      0000000000000011 - 0000000000000011   B   8149acd0
      0000000000000012 - 0000000000000012   B   8149acd0
      0000000000000013 - 0000000000000013   B   8149acd0
      0000000000000014 - 0000000000000014   B   8149acd0
      0000000000000015 - 0000000000000015   B   8149acd0
      0000000000000016 - 0000000000000016   B   8149acd0
      0000000000000017 - 0000000000000017   B   8149acd0
      0000000000000018 - 0000000000000018   B   8149acd0
      0000000000000019 - 0000000000000019   B   8149acd0
      000000000000001a - 000000000000001a   B   8149acd0
      000000000000001b - 000000000000001b   B   8149acd0
      000000000000001c - 000000000000001c   B   8149acd0
      000000000000001d - 000000000000001d   B   8149acd0
 000000000000001e - 000000000000001e   B   8149acd0
      000000000000001f - 000000000000001f   B   8149acd0
 0000000000000020 - 0000000000000020   B   8149acd0
      0000000000000021 - 0000000000000021   B   8149acd0
      0000000000000022 - 0000000000000022   B   8149acd0
      0000000000000023 - 0000000000000023   B   8149acd0
      0000000000000024 - 0000000000000024   B   8149acd0
      0000000000000025 - 0000000000000025   B   8149acd0
      0000000000000026 - 0000000000000026   B   8149acd0
      0000000000000027 - 0000000000000027   B   8149acd0
      0000000000000028 - 0000000000000028   B   8149acd0
      0000000000000029 - 0000000000000029   B   8149acd0
      000000000000002a - 000000000000002a   B   8149acd0
      000000000000002b - 000000000000002b   B   8149acd0
      000000000000002c - 000000000000002c   B   8149acd0
 000000000000002d - 000000000000002d   B   8149acd0
      000000000000002e - 000000000000002e   B   8149acd0
 000000000000002f - 000000000000002f   B   8149acd0
      0000000000000032 - 0000000000000032   B   8149acd0
      0000000000000039 - 0000000000000039 S     814776d0  (ACPI)
    Possible allocation:
      < none >

    DEVNODE 81476f28 (ACPI_HAL\PNP0C08\0)
      Interrupt Arbiter "ACPI_IRQ" at bfff10e0
        Allocated ranges:
          0000000000000000 - 0000000000000000   B   81495bb0
          0000000000000001 - 0000000000000001       814952b0  (i8042prt)
          0000000000000003 - 0000000000000003 S     81495610  (Serial)
          0000000000000004 - 0000000000000004   B   8149acd0
          0000000000000006 - 0000000000000006       81495730  (fdc)
          0000000000000008 - 0000000000000008       81495a90
          0000000000000009 - 0000000000000009 S     814776d0  (ACPI)
          000000000000000b - 000000000000000b S
            000000000000000b - 000000000000000b S     81453c30  (ds1)
            000000000000000b - 000000000000000b S     81453a30  (E100B)
            000000000000000b - 000000000000000b S     81493c30  (uhcd)
            000000000000000b - 000000000000000b S     8145c390  (atirage3)
          000000000000000c - 000000000000000c       814953d0  (i8042prt)
 000000000000000d - 000000000000000d   B   81495850
          000000000000000e - 000000000000000e       8145bb50  (atapi)
 000000000000000f - 000000000000000f       8145b970  (atapi)
        Possible allocation:
          < none > 
```

在这种情况下，将音频、 通用串行总线 (USB)、 网络接口卡 (NIC) 和视频是所有使用相同的 IRQ。

若要找出哪些 ISR 声明中断的所有权，请查看 ISR 的返回值 只需 ISR 使用反汇编**U**命令与地址在 **！ 仲裁器**显示，并在 ISR （它将是 ret 指令） 的最后一个指令处设置断点。 请注意，使用命令**g&lt;地址&gt;** 相当于该地址上设置断点：

```dbgcmd
kd> g bfe33e7b 
ds1wdm!AdapterIsr+ad:
bfe33e7b c20800           ret     0x8 
```

使用**r**命令来检查寄存器。 具体而言，看看 EAX 寄存器。 如果内容中的加粗 （在下面的代码示例） 的寄存器的部分为任何其他然后零，此 ISR 占用了中断。 否则为不声明中断，并且操作系统将调用下一步 ISR 此示例演示视频卡不声明中断：

```dbgcmd
kd> r 
eax=00000000 ebx=813f4ff0 ecx=00000010 edx=ffdff848 esi=8145d168 edi=813f4fc8
eip=bfe33e7b esp=f714eec4 ebp=f714eee0 iopl=0         nv up ei pl zr na po nc
cs=0008  ss=0010  ds=0023  es=0023  fs=0030  gs=0000             efl=00000246
ds1wdm!AdapterIsr+ad:
bfe33e7b c20800           ret     0x8 
```

事实上，在这种情况下，中断不声明任何 IRQ 0xb 上的设备。 当遇到此问题时，还应检查实际是否启用了硬件与中断相关联的每个部分。 对于 PCI，这很容易-查找在显示的 CMD 寄存器 **！ pci**扩展输出：

```dbgcmd
kd> !pci 0 0 
PCI Bus 0
00:0  8086:7190.03  Cmd[0006:.mb...]  Sts[2210:c....]  Device  Host bridge
01:0  8086:7191.03  Cmd[0107:imb..s]  Sts[0220:.6...]  PciBridge 0->1-1  PCI-PCI bridge
03:0  1073:000c.03  Cmd[0000:......]  Sts[0210:c....]  Device  SubID:1073:000c Audio device
04:0  8086:1229.05  Cmd[0007:imb...]  Sts[0290:c....]  Device  SubID:8086:0008 Ethernet
07:0  8086:7110.02  Cmd[000f:imb...]  Sts[0280:.....]  Device  ISA bridge
07:1  8086:7111.01  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
07:2  8086:7112.01  Cmd[0005:i.b...]  Sts[0280:.....]  Device  USB host controller
07:3  8086:7113.02  Cmd[0003:im....]  Sts[0280:.....]  Device  Class:6:80:0 
```

请注意，音频芯片 CMD 注册为零。 这意味着音频芯片有效地禁用这一次。 这也意味着这些音频芯片将不能响应由驱动程序的访问。

在这种情况下，需要手动重新启用音频芯片。

 

 





