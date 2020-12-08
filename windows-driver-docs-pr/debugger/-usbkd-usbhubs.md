---
title: usbkd.usbhubs
description: Usbkd. usbhubs 命令显示有关 USB 集线器的信息。
keywords:
- usbkd usbhubs Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 382bf05fee36e3eee74908824b90e2d3e0c65771
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833213"
---
# <a name="usbkdusbhubs"></a>!usbkd.usbhubs


**！ Usbkd. usbhubs** 命令显示有关 USB 集线器的信息。

```dbgcmd
!usbkd.usbhubs a[v]
!usbkd.usbhubs x[v]
!usbkd.usbhubs r[v]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_____________a"></span><span id="_____________A"></span>**一个**  
显示所有中心。

<span id="_____________r"></span><span id="_____________R"></span>**r**  
显示根中心。

<span id="_____________x"></span><span id="_____________X"></span>**x**  
显示外部中心。

<span id="_____________v"></span><span id="_____________V"></span>**v**  
输出为 verbose。 例如， **！ usbhubs rv** 显示有关所有根集线器的详细输出。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是 **！ usbhubs** 命令的详细输出示例。

```dbgcmd
0: kd> !usbkd.usbhubs rv

args 'rv'
level: r v
ROOT HUBS
*LIST -- Root Hub List @ fffff8000217f440
*flink, blink ffffe000023215c0,ffffe000011f85c0
----------

[0] entry @: ffffe000023201a0
    !DevObj ffffe00002320050 !usbhubext ffffe000023201a0 
On Host Controller (0x8086, 0x293c) 
        Stat_AsyncResumeStartAt: 2437ee39d29bd498
        Stat_AsyncResumeCompleteAt: 24413c77d29bd498
        Stat_AsyncResume: 0x3c(60) ms
        Stat_SyncResumeStartAt: 2437ee39d29bd498
        Stat_SyncResumeCompleteAt: 2437ee39d29bd498
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
##      PortPower_HubStatus : 500

----------

[1] entry @: ffffe000008b91a0
    !DevObj ffffe000008b9050 !usbhubext ffffe000008b91a0 
On Host Controller (0x8086, 0x2937) 
...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

