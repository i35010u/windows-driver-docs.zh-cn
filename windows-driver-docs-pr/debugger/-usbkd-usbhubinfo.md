---
title: usbkd.usbhubinfo
description: Usbkd. hubinfo.h 命令显示有关 USB 集线器的信息。
keywords:
- usbkd usbhubinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f50cff3a178f003992724b848f24520a7cf26097
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829767"
---
# <a name="usbkdusbhubinfo"></a>!usbkd.usbhubinfo


**！ Usbkd. hubinfo.h** 命令显示有关 USB 集线器的信息。

```dbgcmd
!usbkd.hubinfo FDO
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______FDO______"></span><span id="_______fdo______"></span>*FDO*   
USB 集线器 (FDO) 的功能设备对象的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找 USB 集线器的 FDO 地址的一种方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
```

在上面的输出中，中心的 FDO 地址显示为建议的命令 **！ devstack ffffe00002320050** 的参数。

现在，将 FDO 的地址传递给 **！ usbhubinfo** 命令。

```dbgcmd
0: kd> !usbkd.usbhubinfo ffffe00002320050

    !DevObj ffffe00002320050 !usbhubext ffffe000023201a0 
On Host Controller (0x8086, 0x293c) 
        Stat_AsyncResumeStartAt: 2437ee39d29bd528
        Stat_AsyncResumeCompleteAt: 24413c77d29bd528
        Stat_AsyncResume: 0x3c(60) ms
        Stat_SyncResumeStartAt: 2437ee39d29bd528
        Stat_SyncResumeCompleteAt: 2437ee39d29bd528
        Stat_SyncResume: 0x0(0) ms
Trap Regs: Event, Port, Event (ffffe000023204d0) 
    Enable: 0 Port: 0 Event 00000000
Hub Number: # 3
Number Of Ports: 4
dt usbhub!_USBHUB_FDO_FLAGS ffffe00002320ba0
>Is Root
>Power Switching: 
     No Power Switching 
>Overcurrent: 
     Global Overcurrent 
>PortIndicators: 
     No PortIndicators present
>AllowWakeOnConnect: 
     DO NOT WakeOnConnect
>CURRENT Hub Wake on Connectstate: 
     HWC_DISARM:- do not wake system on connect/disconnect event
>CURRENT Bus Wake state: 
     BUS_DISARM:- bus not armed for wake by this hub
>CURRENT Wake Detect state (WW Irp): 
     HUB_DISARM:- no ww irp pending (HUB_WAKESTATE_DISARMED)
Milliamps/Port : 500ma
Power caps (0 = not reported)
     PortPower_Registry : 0
     PortPower_DeviceStatus : 500
     PortPower_CfgDescriptor : 500
     PortPower_HubStatus : 500
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

