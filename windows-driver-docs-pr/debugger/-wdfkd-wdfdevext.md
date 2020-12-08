---
title: wdfkd.wdfdevext
description: Wdfdevext 扩展显示与 Microsoft Windows 驱动模型 (WDM) DEVICE_OBJECT 结构的 DeviceExtension 成员关联的信息。
keywords:
- wdfkd wdfdevext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfdevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ccc46cedc921b7f206ef02e99840d7dd5b572c56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814621"
---
# <a name="wdfkdwdfdevext"></a>!wdfkd.wdfdevext


**！ Wdfkd wdfdevext** 扩展显示与 Microsoft WINDOWS 驱动模型 (WDM) 设备对象结构的 **DeviceExtension** 成员关联的信息 \_ 。

```dbgcmd
!wdfkd.wdfdevext DeviceExtension
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
指向设备扩展的指针。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>协作

KMDF 1，UMDF 1，UMDF 2

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核模式驱动程序框架调试](kernel-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面是一个 KMDF 驱动程序 HdAudBus.sys 的示例。 使用 [**！ devnode**](-devnode.md) 查找将 HdAudBus 作为其函数驱动程序的设备节点。 从输出中获取 (PDO) 的物理设备对象，并将其传递到 [**！ devstack**](-devstack.md)。 从 **！ devstack** 的输出中获取设备扩展地址，并将其传递给 **！ wdfdevext**。

```dbgcmd
0: kd> !devnode 0 1 hdaudbus
Dumping IopRootDeviceNode (= 0xffffe000002cfd30)
DevNode 0xffffe000009b7a50 for PDO 0xffffe00000226880
  InstancePath is "PCI\VEN_8086&DEV_293E&SUBSYS_2819103C&REV_02\3&33fd14ca&0&D8"
  ServiceName is "HDAudBus"
  ...
0: kd> !devstack 0xffffe00000226880
  !DevObj           !DrvObj            !DevExt           ObjectName
  ffffe00001351e20  \Driver\HDAudBus   ffffe000009a3c00  
> ffffe00000226880  \Driver\pci        ffffe000002269d0  NTPNP_PCI0009
!DevNode ffffe000009b7a50 :
  DeviceInst is "PCI\VEN_8086&DEV_293E&SUBSYS_2819103C&REV_02\3&33fd14ca&0&D8"
  ServiceName is "HDAudBus"
0: kd> *
0: kd> !wdfdevext ffffe000009a3c00
Device context is 0xffffe000009a3c00
    context:  dt 0xffffe000009a3c00 HDAudBus!HDAudioDeviceExtension (size is 0xa8 bytes)
    EvtCleanupCallback fffff80001f35950 HDAudBus!HdAudBusEvtDeviceCleanupCallback

!wdfdevice 0x00001fffff65c6e8                        
!wdfobject 0xffffe000009a3910
```

下面是 Wudfrd.sys 的示例，它是 UMDF 2 驱动程序堆栈的内核模式部分的函数驱动程序。 使用 [**！ devnode**](-devnode.md) 查找将 Wudfrd 作为其函数驱动程序的设备节点。 从输出中获取 (PDO) 的物理设备对象，并将其传递到 [**！ devstack**](-devstack.md)。 从 **！ devstack** 的输出中获取设备扩展地址，并将其传递给 **！ wdfdevext**。

```dbgcmd
0: kd> !devnode 0 1 wudfrd
Dumping IopRootDeviceNode (= 0xffffe000002cfd30)
DevNode 0xffffe00000a1e530 for PDO 0xffffe00000b15b00
  InstancePath is "ROOT\SAMPLE\0001"
  ServiceName is "WUDFRd"
  ...
0: kd> !devstack 0xffffe00000b15b00
  !DevObj           !DrvObj            !DevExt           ObjectName
  ffffe00000c11040  \Driver\WUDFRd     ffffe00000c11190  
> ffffe00000b15b00  \Driver\PnpManager 00000000  00000052
!DevNode ffffe00000a1e530 :
  DeviceInst is "ROOT\SAMPLE\0001"
  ServiceName is "WUDFRd"
0: kd> *
0: kd> !wdfdevext ffffe00000c11190
## Device context is 0xffffe00000c11190

##  UMDF Device Instances for this Redirector extension

  DriverManagerProcess: 0xffffe00003470500

  ImageName              Ver   DevStack           HostProcess        DeviceID      
  MyUmdf2Driver.dll      v2.0  0x000000a5a3ab5f70 0xffffe00000c32900  \Device\00000052
```

 

 





