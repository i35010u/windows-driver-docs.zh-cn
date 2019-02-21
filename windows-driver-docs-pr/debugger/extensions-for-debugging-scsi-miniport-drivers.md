---
title: SCSI 微型端口驱动程序调试扩展
description: SCSI 微型端口驱动程序调试扩展
ms.assetid: 6e6c35e5-d9dd-430a-8fc4-86f24344c24d
keywords:
- SCSI 微型端口调试，有用的扩展
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6cc9c9db0203cd571eb22d24eb88b9632115032
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521548"
---
# <a name="extensions-for-debugging-scsi-miniport-drivers"></a>SCSI 微型端口驱动程序调试扩展


当调试 SCSI 微型端口驱动程序时，可能会发现以下调试器扩展很有用。 常规调试器扩展会首先列出后, 跟的那些特定 SCSI 微型端口调试。

[**!devobj**](-devobj.md)  
**！ Devobj**扩展插件都会显示有关设备的详细的信息\_对象。 如果**当前 Irp**字段为非 null，这可能由 SCSI 驱动程序等待映射注册。

下面是一个示例：

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
**！ Errlog**扩展 I/O 系统错误日志中显示的任何挂起的项的内容。

[**!object**](-object.md)  
**！ 对象**扩展显示有关系统对象的信息。 此扩展显示所有 SCSI 设备。

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
**！ Pcr**扩展处理器上显示有关处理器控件区域 (PCR) 的详细的信息。 信息包括在 DPC 队列中，这可能很有用的项目。 在调试已停止的驱动程序或超时。

[**!minipkd.help**](-minipkd-help.md)  
**！ Minipkd.help**扩展插件都会显示所有 Minipkd.dll 扩展命令的列表。

如果出现类似于以下错误消息，它指示符号路径不正确，并且不指向 Scsiport.sys 符号的正确版本。

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

[ **.Sympath （设置符号路径）** ](-sympath--set-symbol-path-.md)可以使用命令，以显示当前路径以及更改的路径。 [ **.Reload （重新加载模块）** ](-reload--reload-module-.md)命令将重新加载当前路径中的符号。

[**!minipkd.adapter Adapter**](-minipkd-adapter.md)  
**！ Minipkd.adapter**扩展显示有关指定的适配器的详细的信息。 **适配器**可以通过查看找到**DevExt**字段中 **！ minipkd.adapters**显示。

[**!minipkd.adapters**](-minipkd-adapters.md)  
**！ Minipkd.adapters**扩展显示的所有适配器使用 SCSI 端口驱动程序的已发现的 Windows，并与每个适配器关联的单个设备。

下面是一个示例：

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

类似于以下错误消息表示的符号路径不正确，并且不指向 Scsiport.sys 符号的正确版本或 Windows 未标识任何使用 SCSI 端口驱动程序的适配器：

```dbgcmd
minipkd error (0) <path> ... \minipkd\minipkd.c @ line 435
```

如果[ **！ minipkd.help** ](-minipkd-help.md)扩展命令返回的帮助信息已成功，SCSI 端口符号是否正确。

[**!minipkd.exports Adapter**](-minipkd-exports.md)  
**！ Minipkd.exports**扩展显示指定的适配器的微型端口导出结果的地址。

[**!minipkd.lun {LUN | Device}**](-minipkd-lun.md)  
**！ Minipkd.lun**扩展显示有关指定的逻辑单元扩展 (LUN) 的详细的信息。 LUN 可以是指定的地址 (可以通过查看找到**LUN**字段中 **！ minipkd.adapters**显示) 或由其物理设备对象 (但可以参阅**DevObj**字段 **！ minipkd.adapters**显示)。

[**!minipkd.portconfig PortConfig**](-minipkd-portconfig.md)  
**！ Minipkd.portconfig**扩展插件都会显示有关指定的端口的详细的信息\_配置\_数据。 **PortConfig**中可以找到**端口配置信息**字段 **！ minipkd.adapter**显示。

[**!minipkd.req {Adapter | Device}**](-minipkd-req.md)  
**！ Minipkd.req**扩展指定的适配器或 LUN 设备上显示所有当前处于活动状态的请求有关的信息。

[**!minipkd.srb SRB**](-minipkd-srb.md)  
**！ Minipkd.srb**扩展显示有关指定的 SCSI 请求块 (SRB) 的详细的信息。 SRB 被指定的地址。 当前处于活动状态的所有请求的地址可在**SRB**的输出字段 **！ minipkd.req**命令。

[**！ scsikd.classext\[设备\[级别\]\]**](-scsikd-classext.md)  
**！ Scsikd.classext**扩展显示有关指定的类插即用 (PnP) 设备或一组所有此类设备的详细的信息。 *设备*设备对象或类即插即用设备的设备扩展。 如果*设备*是省略，将显示所有类即插即用扩展的列表。

下面是一个示例：

```dbgcmd
0: kd> !scsikd.classext 

 ' !scsikd.classext 8633e3f0 '   (             ) "IBM     " / "DDYS-T09170M    " / "S93E" / "        XBY45906"
 ' !scsikd.classext 86347b48 '   (paging device) "IBM     " / "DDYS-T09170M    " / "S80D" / "        VDA60491"
  ' !scsikd.classext 86347360 '   (             ) "UNISYS  " / "003451ST34573WC " / "5786" / "HN0220750000181300L6"
  ' !scsikd.classext 861d1898 '   (             ) "" / "MATSHITA CD-ROM CR-177" / "7T03" / ""

 usage: !classext <class fdo> <level [0-2]> 
```

[**！ scsikd.scsiext 设备**](-scsikd-scsiext.md)  
**！ Scsikd.scsiext**扩展显示有关指定的 SCSI 端口扩展的详细的信息。 *设备*可以是设备对象或设备适配器或 LUN 的扩展。

下面提供了一些示例：

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

[**!scsikd.srbdata Address**](-scsikd-srbdata.md)  
**！ Scsikd.srbdata**扩展显示详细的信息指定 SRB\_数据跟踪块。

 

 





