---
title: 用于调试即插即用驱动程序的扩展
description: 用于调试即插即用驱动程序的扩展
keywords:
- 即插即用 (PnP) 、扩展
- 扩展，即插即用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b78c90c7016ca4432d79f2075d163ff069262c64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840207"
---
# <a name="extensions-for-debugging-plug-and-play-drivers"></a>用于调试即插即用驱动程序的扩展


调试即插即用驱动程序时，可能会发现以下调试器扩展很有用。

[**!arbiter**](-arbiter.md)  
显示当前系统资源的仲裁器。 仲裁器是由总线驱动程序公开的一段代码，用于仲裁资源的请求，并尝试解决在该总线上连接的设备之间的资源冲突。

[**!cmreslist**](-cmreslist.md)  
显示 \_ \_ 指定设备对象的 CM 资源列表。

您必须知道 CM 资源列表的地址。

以下是示例：

```dbgcmd
kd> !cmreslist 0xe12576e8

CmResourceList at 0xe12576e8  Version 0.0  Interface 0x1  Bus #0
  Entry 0 - Port (0x1) Device Exclusive (0x1)
    Flags (0x01) - PORT_MEMORY PORT_IO
    Range starts at 0x3f8 for 0x8 bytes
  Entry 1 - Interrupt (0x2) Shared (0x3)
    Flags (0x01) - LATCHED
    Level 0x4, Vector 0x4, Affinity 0xffffffff
```

这表明具有此 CM 资源列表的设备使用 i/o 范围 3F8-3FF 和 IRQ 4。

[**!dcs**](-dcs.md)  
此扩展已过时--它的功能已被归入 [**！ pci**](-pci.md)。 请参阅本部分后面的！ pci 100 示例。

[**!devext**](-devext.md)  
显示各种设备的特定于总线的设备扩展信息。

[**!devnode**](-devnode.md)  
显示有关设备树中的节点的信息。

设备节点 0 (零) 是设备树的根。

以下是示例：

```dbgcmd
0: kd> !devnode 0xfffffa8003634af0
DevNode 0xfffffa8003634af0 for PDO 0xfffffa8003658590
  Parent 0xfffffa8003604010   Sibling 0xfffffa80036508e0   Child 0000000000
  InstancePath is "ROOT\SYSTEM\0000"
  ServiceName is "swenum"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[09] = DeviceNodeEnumerateCompletion (0x30d)
  StateHistory[08] = DeviceNodeEnumeratePending (0x30c)
  StateHistory[07] = DeviceNodeStarted (0x308)
  StateHistory[06] = DeviceNodeStartPostWork (0x307)
  StateHistory[05] = DeviceNodeStartCompletion (0x306)
  StateHistory[04] = DeviceNodeStartPending (0x305)
  ...
  Flags (0x6c000131)  DNF_MADEUP, DNF_ENUMERATED, 
                      DNF_IDS_QUERIED, DNF_NO_RESOURCE_REQUIRED, 
                      DNF_NO_LOWER_DEVICE_FILTERS, DNF_NO_LOWER_CLASS_FILTERS, 
                      DNF_NO_UPPER_DEVICE_FILTERS, DNF_NO_UPPER_CLASS_FILTERS
  UserFlags (0x00000008)  DNUF_NOT_DISABLEABLE
  DisableableDepends = 1 (including self)
```

[**!devobj**](-devobj.md)  
显示有关设备对象的详细信息 \_ 。

以下是示例：

```dbgcmd
kd> !devobj 0xff0d4af0

Device object (ff0d4af0) is for:
 00252d \Driver\PnpManager DriverObject ff0d9030
Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001040AttachedDev ff0b59e0

DevExt ff0d4ba8 DevNode ff0d4a08
Device queue is not busy.
```

[**！个驱动程序**](-drivers.md)  
不再支持 [**！！驱动程序**](-drivers.md) 命令。 改为使用 [**lm t n**](lm--list-loaded-modules-.md) 命令。

[**!drvobj**](-drvobj.md)  
显示有关驱动程序对象的详细信息 \_ 。

列出由指定的驱动程序创建的所有设备对象。

以下是示例：

```dbgcmd
kd> !drvobj serial

Driver object (ff0ba630) is for:
 \Driver\Serial
Driver Extension List: (id , addr)

Device Object list:
ffba3040  ff0b4040  ff0b59e0  ff0b5040
```

[**!ecb、!ecd、!ecw**](-ecb---ecd---ecw.md)  
 (x86 目标计算机仅) 将一系列值写入 PCI 配置空间。

[**ib，iw，id**](-ib---id---iw.md)  
从 i/o 端口读取数据。

这三个命令可用于确定某个 i/o 范围是否由正在调试的驱动程序以外的其他设备所声称。 端口上的值为0xFF 表示端口未被使用。

[**!ioreslist**](-ioreslist.md)  
显示指定的 IO \_ 资源 \_ 需求 \_ 列表。

[**!irp**](-irp.md)  
显示 IRP 的相关信息。

[**!irpfind**](-irpfind.md)  
显示有关目标系统中当前分配的所有 Irp 的信息，或有关其字段与指定搜索条件匹配的那些 Irp 的信息。

[**!pci**](-pci.md)  
 (x86 目标计算机仅) 显示 PCI 总线和附加到它们的任何设备的当前状态。 它还可以显示 PCI 配置空间。

以下示例显示了主总线上的设备：

```dbgcmd
kd> !pci
PCI Bus 0
00:0  8086:1237.02  Cmd[0106:.mb..s]  Sts[2280:.....]  Device  Host bridge
0d:0  8086:7000.01  Cmd[0007:imb...]  Sts[0280:.....]  Device  ISA bridge
0d:1  8086:7010.00  Cmd[0005:i.b...]  Sts[0280:.....]  Device  IDE controller
0e:0  1011:0021.01  Cmd[0107:imb..s]  Sts[0280:.....]  PciBridge 0->1-1  PCI-PCI
 bridge
10:0  5333:8811.43  Cmd[0023:im.v..]  Sts[0200:.....]  Device  VGA compatible controller



The following example displays the devices for the secondary bus, with verbose output:

kd> !pci 1 1

PCI Bus 1
08:0  10b7:5900.00  Cmd[0107:imb..s]  Sts[0200:.....]  Device  Ethernet
      cf8:80014000  IntPin:1  IntLine:f  Rom:fa000000  cis:0  cap:0
      IO[0]:fce1

09:0  9004:8178.00  Cmd[0117:imb..s]  Sts[0280:.....]  Device  SCSI controller
      cf8:80014800  IntPin:1  IntLine:f  Rom:fa000000  cis:0  cap:0
      IO[0]:f801       MEM[1]:f9fff000

0b:0  9004:5800.10  Cmd[0116:.mb..s]  Sts[0200:.....]  Device  SubID:9004:8940
1394 host controller
      cf8:80015800  IntPin:1  IntLine:e  Rom:fa000000  cis:0  cap:0
      MEM[0]:f9ffec00
```

以下示例显示了 SCSI 控制器 (总线1、设备9、函数 0) 的 PCI 配置空间：

```dbgcmd
kd> !pci 100 1 9 0 
00: 9004    ;VendorID=9004
02: 8178    ;DeviceID=8178
04: 0117    ;Command=SERREnable,MemWriteEnable,BusInitiate,MemSpaceEnable,IOSpac
eEnable
06: 0280    ;Status=FB2BCapable,DEVSELTiming:1
08: 00      ;RevisionID=00
09: 00      ;ProgIF=00 (SCSI bus controller)
0a: 00      ;SubClass=00
0b: 01      ;BaseClass=01 (Mass storage controller)
0c: 08      ;CacheLineSize=Burst8DW
0d: 20      ;LatencyTimer=20
0e: 00      ;HeaderType=00
0f: 00      ;BIST=00
10: 0000f801;BAR0=0000f801
14: f9fff000;BAR1=f9fff000
18: 00000000;BAR2=00000000
1c: 00000000;BAR3=00000000
20: 00000000;BAR4=00000000
24: 00000000;BAR5=00000000
28: 00000000;CBCISPtr=00000000
2c: 0000    ;SubSysVenID=0000
2e: 0000    ;SubSysID=0000
30: fa000000;ROMBAR=fa000000
34: 00000000;Reserved=00000000
38: 00000000;Reserved=00000000
3c: 0f      ;IntLine=0f
3d: 01      ;IntPin=01
3e: 08      ;MinGnt=08
3f: 08      ;MaxLat=08
40: 00001580,00001580,00000000,00000000,00000000,00000000,00000000,00000000
60: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
80: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
a0: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
c0: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
e0: 00000000,00000000,00000000,00000000,00000000,00000000,00000000,00000000
```

[**!pcitree**](-pcitree.md)  
显示有关 PCI 设备对象的信息，包括子 PCI 总线和 CardBus 总线，以及连接到它们的设备。

[**!pnpevent**](-pnpevent.md)  
显示 PnP 设备事件队列。

[**!rellist**](-rellist.md)  
显示 PnP 关系列表以及任何相关的 CM \_ 资源 \_ 列表和 IO \_ 资源 \_ 列表结构。

 

 





