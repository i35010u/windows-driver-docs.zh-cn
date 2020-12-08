---
title: wdfkd.wdfldr
description: Wdfkd. wdfldr 扩展显示有关当前动态绑定到 Windows 驱动程序框架的 KMDF 和 UMDF 驱动程序的信息。
keywords:
- wdfkd wdfldr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfldr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3f963273da45cf502ed5ac87c8736ced94ac923
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838387"
---
# <a name="wdfkdwdfldr"></a>!wdfkd.wdfldr


**！ Wdfkd wdfldr** 扩展显示有关当前动态绑定到 Windows 驱动程序框架的驱动程序的信息。 这包括 Kernel-Mode Driver Framework (KMDF) 和 User-Mode Driver Framework (UMDF) 。

```dbgcmd
!wdfkd.wdfldr [DriverName]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span>*DriverName*   
驱动程序的名称，包括文件扩展名。 如果提供驱动程序名称，则此命令将显示有关一个驱动程序的详细信息。 如果未提供驱动器名称，则此命令将显示有关绑定到 Windows 驱动程序框架的所有驱动程序的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面是 **！ wdfldr** 的输出示例。

```dbgcmd
## 0: kd> !wdfkd.wdfldr

##  KMDF Drivers

##  LoadedModuleList      0xfffff800003b61f8

LIBRARY_MODULE  0xffffe0000039f7c0
  Version       v1.13
  Service       \Registry\Machine\System\CurrentControlSet\Services\Wdf01000
  ImageName     Wdf01000.sys
  ImageAddress  0xfffff800002e7000
  ImageSize     0xc5000
  Associated Clients: 16

  ImageName                      Ver   WdfGlobals         FxGlobals          ImageAddress       ImageSize
  peauth.sys                     v1.7  0xffffe00003a95880 0xffffe00003a956e0 0xfffff80002678000 0x000ab000
  monitor.sys                    v1.11 0xffffe000001abc70 0xffffe000001abad0 0xfffff800022e7000 0x0000e000
  UsbHub3.sys                    v1.11 0xffffe000028a47b0 0xffffe000028a4610 0xfffff8000220b000 0x00077000
##   ...

## Total: 1 library loaded

##  UMDF Drivers

  DriverManagerProcess: 0xffffe00003470500

  ImageName                      Ver
  MyUmdfDriver.dll               v1.11 
  SomeUmdf2Driver.dll            v2.0  
  MyUmdf2Driver.dll              v2.0
```

下面是提供驱动程序名称的另一个示例。

```dbgcmd
0: kd> !wdfldr MyUmdf2Driver.dll

Version    v2.0
Service    \Registry\Machine\System\CurrentControlSet\Services\MyUmdf2Driver

## !wdflogdump  MyUmdf2Driver.dll

##  UMDF Device Instances using MyUmdf2Driver.dll

Process             DevStack           DeviceId
0xffffe00000c32900  a5a3ab5f70         \Device\00000052 !wdfdriverinfo
```

 

 





