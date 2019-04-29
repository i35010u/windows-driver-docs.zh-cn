---
title: 分析已停止的驱动程序和超时
description: 分析已停止的驱动程序和超时
ms.assetid: c305acba-48b9-4597-925a-8b1ded4f0048
keywords:
- SCSI 微型端口调试、 挂起和超时值
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191bda869710e14d445e68722da54c06c9d08290
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355411"
---
# <a name="analyzing-stalled-drivers-and-time-outs"></a>分析已停止的驱动程序和超时


在调试时 SCSI 微型端口驱动程序，三个最常见原因挂起和超时设置：

-   SCSI 微型端口 DPC 未运行

-   SCSI 微型端口失败请求的下一个请求

-   SCSI 微型端口不完成一项请求，则通常因为它正在等待映射注册。

如果你怀疑，SCSI 微型端口 DPC 未运行，使用[ **！ pcr** ](-pcr.md)以显示当前处理器的 DPC 队列。 如果 SCSI 端口 DPC 例程 DPC 队列中，此例程，以确定是否曾经调用该例程上放置一个断点。 否则，请使用[ **！ scsikd.scsiext** ](-scsikd-scsiext.md)每台设备上。 请考虑从下面的示例输出 **！ scsikd.scsiext**扩展：

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

如果超时槽为-1 和未标记的槽不为零，或超时槽为非零值且没有请求所示，微型端口失败请求的下一个请求。

或者，如果重试槽和忙槽不为零时，请求可能无法完成通过 SCSI 微型端口因为它正在等待映射寄存器。 同样，如果未标记和挂起的槽不为零时，SCSI 微型端口可能正在等待映射寄存器。 在任一情况下，SCSI 请求块 (SRB) 的地址是繁忙的槽中的地址和未完成该请求的地址。 有关 SRB 的详细信息，请使用[ **！ minipkd.srb** ](-minipkd-srb.md)扩展与作为输入此地址。

[ **！ Devobj** ](-devobj.md)扩展插件确定 SCSI 微型端口是否正在等待的映射注册。 使用的作为输入发出请求的设备的设备对象地址 **！ devobj**。 如果当前 IRQ 不为零，则高可能 SCSI 微型端口正在等待映射寄存器。

 

 





