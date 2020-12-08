---
title: 用于调试 SCSI 微型端口驱动程序的扩展
description: 用于调试 SCSI 微型端口驱动程序的扩展
keywords:
- SCSI 微型端口调试，有用的扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46627ea77d5304cbeeb66f2c675852593e96a10c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840205"
---
# <a name="extensions-for-debugging-scsi-miniport-drivers"></a>用于调试 SCSI 微型端口驱动程序的扩展


调试 SCSI 微型端口驱动程序时，可能会发现以下调试器扩展很有用。 首先列出常规调试器扩展，然后列出特定于 SCSI 微型端口调试的扩展。

[**!devobj**](-devobj.md)  
**！ Devobj** 扩展显示有关设备对象的详细信息 \_ 。 如果 **当前 Irp** 字段为非空，则这可能是由于 SCSI 驱动程序正在等待映射寄存器导致的。

以下是示例：

```dbgcmd
0: kd> !devobj 8633da70
Device object (8633da70) is for:
 adpu160m1 \Driver\adpu160m DriverObject 8633eeb8
Current Irp 860ef008 RefCount 0 Type 00000004 Flags 00000050
Dacl e129871c DevExt 8633db28 DevObjExt 8633dfd0
ExtensionFlags (0000000000)
AttachedTo (Lower) 863b2978 \Driver\PCI
Device queue is not busy. 
```

[**!errlog**](-errlog.md)  
**！ .Errlog** extension 显示 i/o 系统的错误日志中任何挂起项的内容。

[**！对象**](-object.md)  
**！对象** 扩展显示有关系统对象的信息。 此扩展显示所有 SCSI 设备。

例如：

```dbgcmd
0: kd> !object \device\scsi
Object: e12a2520  Type: (863d12c8) Directory
    ObjectHeader: e12a2508
    HandleCount: 0  PointerCount: 9
    Directory Object: e1001100  Name: Scsi

    Hash Address  Type          Name
    ---- -------  ----          ----
     04  86352040 Device        adpu160m1Port3Path0Target6Lun0
     11  86353040 Device        adpu160m1Port3Path0Target1Lun0
     13  86334a70 Device        lp6nds351
     22  862e6040 Device        adpu160m1Port3Path0Target0Lun0
     24  8633da70 Device        adpu160m1
     25  86376040 Device        adpu160m2
     34  862e5040 Device        adpu160m1Port3Path0Target2Lun0 
```

[**!pcr**](-pcr.md)  
**！ Pcr** 扩展显示处理器上 (pcr) 的处理器控制区域的详细信息。 此信息包括 DPC 队列中的项目，这会很有用。 调试停止的驱动程序或超时。

[**!minipkd.help**](-minipkd-help.md)  
**！ Minipkd** 显示所有 Minipkd.dll 扩展命令的列表。

如果出现类似于下面的错误消息，则表示符号路径不正确，并且不指向正确的 Scsiport.sys 符号版本。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

可以使用 [**sympath (设置符号路径)**](-sympath--set-symbol-path-.md) 命令来显示当前路径并更改路径。 Reload.sql [**(Reload.sql Module)**](-reload--reload-module-.md) 命令将从当前路径重新加载符号。

[**！ minipkd 适配器**](-minipkd-adapter.md)  
**！ Minipkd** 扩展显示有关指定适配器的详细信息。 可以通过查看 **！ minipkd** 显示中的 **DevExt** 字段来找到 **适配器**。

[**!minipkd.adapters**](-minipkd-adapters.md)  
**！ Minipkd** 扩展显示与 Windows 标识的 SCSI 端口驱动程序一起使用的所有适配器，以及与每个适配器关联的各个设备。

以下是示例：

```dbgcmd
0: kd> !minipkd.adapters
Adapter \Driver\lp6nds35     DO 86334a70         DevExt 86334b28
Adapter \Driver\adpu160m     DO 8633da70         DevExt 8633db28
 LUN 862e60f8 @(0,0,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e6040
 LUN 863530f8 @(0,1,0) c ev p d pnp(00/ff) pow(0,0) DevObj 86353040
 LUN 862e50f8 @(0,2,0) c ev     pnp(00/ff) pow(0,0) DevObj 862e5040
 LUN 863520f8 @(0,6,0)   ev     pnp(00/ff) pow(0,0) DevObj 86352040
Adapter \Driver\adpu160m     DO 86376040         DevExt 863760f8 
```

类似于下面的错误消息指示符号路径不正确，并且未指向正确版本的 Scsiport.sys 符号，或者 Windows 尚未识别使用 SCSI 端口驱动程序的任何适配器：

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

如果 [**！ minipkd**](-minipkd-help.md) extension 命令成功返回帮助信息，则 SCSI 端口符号正确。

[**！ minipkd 适配器**](-minipkd-exports.md)  
**！ Minipkd** extension 显示指定适配器的微型端口导出地址。

[**！ minipkd {LUN |装置**](-minipkd-lun.md)  
**！ Minipkd** 扩展显示 (lun) 的指定逻辑单元扩展的详细信息。 可以 (通过以下方式指定 LUN：通过查看 **！ minipkd** 显示屏中的 **LUN** 字段) 或它的物理设备对象来指定该 lun (可在 **！ minipkd** 显示) 的 **DevObj** 字段中找到该字段。

[**!minipkd.portconfig PortConfig**](-minipkd-portconfig.md)  
**！ Minipkd portconfig** 扩展显示有关指定端口配置数据的详细信息 \_ \_ 。 可以在 **！ minipkd** 显示的 "**端口配置信息**" 字段中找到 **PortConfig** 。

[**！ minipkd {Adapter |装置**](-minipkd-req.md)  
**！ Minipkd** 扩展显示有关指定适配器或 LUN 设备上所有当前活动的请求的信息。

[**!minipkd.srb SRB**](-minipkd-srb.md)  
**！ Minipkd srb** (srb) 中显示有关指定 SCSI 请求块的详细信息。 SRB 由 address 指定。 可以在 **！ minipkd** 命令的输出的 **SRB** 字段中找到所有当前活动的请求的地址。

[**！ scsikd classext \[ 设备 \[ 级别\]\]**](-scsikd-classext.md)  
**！ Scsikd classext** 扩展显示有关指定类即插即用 (PnP) 设备或所有此类设备的列表的详细信息。 *设备* 是类 PnP 设备的设备对象或设备扩展。 如果省略 *设备* ，则显示所有类 PnP 扩展的列表。

以下是示例：

```dbgcmd
0: kd> !scsikd.classext 

 ' !scsikd.classext 8633e3f0 '   (             ) "IBM     " / "DDYS-T09170M    " / "S93E" / "        XBY45906"
 ' !scsikd.classext 86347b48 '   (paging device) "IBM     " / "DDYS-T09170M    " / "S80D" / "        VDA60491"
  ' !scsikd.classext 86347360 '   (             ) "UNISYS  " / "003451ST34573WC " / "5786" / "HN0220750000181300L6"
  ' !scsikd.classext 861d1898 '   (             ) "" / "MATSHITA CD-ROM CR-177" / "7T03" / ""

 usage: !classext <class fdo> <level [0-2]> 
```

[**！ scsikd scsiext 设备**](-scsikd-scsiext.md)  
**！ Scsikd scsiext** 扩展显示有关指定 SCSI 端口扩展的详细信息。 *设备* 可以是适配器或 LUN 的设备对象或设备扩展。

下面是一些示例：

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
  < ..omitted.. >
Request list @0x86353200:
      Tick count is 2526
      SrbData 8615d700  Srb 8611f4fc  Irp 8611f2b8   Key 60197  <1s
      SrbData 85e72868  Srb 86100c3c Irp 861009f8   Key e29dc7  <1s

0: kd> !scsikd.scsiext 8633da70 
Common Extension:
   < ..omitted.. >
Adapter Extension:
  Port 3     IsPnp VirtualSlot HasInterrupt
  LowerPdo 0x84f9fb68   HwDevExt 0x84634004   Active Requests 0x00000000
  MaxBus 0x03   MaxTarget 0x40   MaxLun 0x08
  Port Flags (0x00001000): PD_DISCONNECT_RUNNING
  NonCacheExt 0x850d4000  IoBase 0xd80f0000   Int 0x23  < ..omitted.. > 
```

[**！ scsikd. srbdata Address**](-scsikd-srbdata.md)  
**！ Scsikd srbdata** 扩展显示有关指定 SRB \_ 数据跟踪块的详细信息。

 

 





