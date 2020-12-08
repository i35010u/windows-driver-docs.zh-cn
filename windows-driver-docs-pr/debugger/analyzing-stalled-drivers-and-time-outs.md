---
title: 分析已停止的驱动程序和超时
description: 分析已停止的驱动程序和超时
keywords:
- SCSI 微型端口调试、挂起和超时
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cad0c54ae355125964078db3a4c2dd7a421db09
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819327"
---
# <a name="analyzing-stalled-drivers-and-time-outs"></a>分析已停止的驱动程序和超时


调试 SCSI 微型端口驱动程序时，挂起和超时的三个最常见的原因如下：

-   SCSI 微型端口 DPC 未运行

-   SCSI 微型端口无法要求下一个请求

-   SCSI 微型端口不会完成请求，通常是因为它正在等待映射寄存器。

如果怀疑 SCSI 微型端口 DPC 未运行，请使用 [**！ pcr**](-pcr.md) 显示当前处理器的 DPC 队列。 如果 SCSI 端口 DPC 例程在 DPC 队列中，请在此例程上放置一个断点，以确定是否曾经调用过此例程。 否则，请在每个设备上使用 [**！ scsikd。**](-scsikd-scsiext.md) 请考虑以下来自 **！ scsikd. scsiext** 扩展的示例输出：

```dbgcmd
0: kd> !scsikd.scsiext 86353040 
Common Extension:
   < ..omitted.. >
Logical Unit Extension:
  Address (3, 0, 1, 0) Claimed  Enumerated Visible
  LuFlags (0x00000000):
  Retry 0x00          Key 0x008889ff
  Lock 0x00000000  Pause 0x00000000   CurrentLock: 0x00000000
  HwLuExt 0x862e6f00  Adapter 0x8633db28  Timeout 0x0000000a
  NextLun 0x00000000  ReadyLun 0x00000000
  Pending 0x00000000  Busy 0x00000000     Untagged 0x00000000
 
  . . .  
 
Request list @0x86353200:
      Tick count is 2526
      SrbData 8615d700  Srb 8611f4fc  Irp 8611f2b8   Key 60197  <1s
      SrbData 85e72868  Srb 86100c3c Irp 861009f8   Key e29dc7  <1s 
```

如果超时槽为-1，未标记的槽为非零值，或者超时槽为非零值并且显示了个请求，则该微型端口未能要求下一个请求。

或者，如果重试槽和忙槽为非零，则 SCSI 微型端口可能不会完成请求，因为该请求正在等待映射寄存器。 同样，如果未标记和挂起的槽为非零，则 SCSI 微型端口可能会等待映射寄存器。 在任一情况下，SCSI 请求块的地址 (SRB) 是繁忙插槽中的地址和未完成的请求的地址。 有关 SRB 的详细信息，请使用带有此地址的 [**！ minipkd**](-minipkd-srb.md) 作为输入。

[**！ Devobj**](-devobj.md) EXTENSION 确定 SCSI 微型端口是否正在等待映射寄存器。 将发出请求的设备的设备对象地址作为输入到 **！ devobj**。 如果当前 IRQ 为非零，则很可能 SCSI 微型端口正在等待映射寄存器。

 

 





