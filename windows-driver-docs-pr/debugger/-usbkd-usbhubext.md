---
title: usbkd.usbhubext
description: Usbkd. usbhubext 命令显示有关 USB 集线器的信息。
keywords:
- usbkd usbhubext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e24ddc093d97121760545eb56c70ee6200133a1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829771"
---
# <a name="usbkdusbhubext"></a>!usbkd.usbhubext


**！ Usbkd. usbhubext** 命令显示有关 USB 集线器的信息。

```dbgcmd
!usbkd.usbhubext DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
以下项之一的地址：

-   功能设备对象的设备扩展 (USB 集线器的 FDO) 。
-    (PDO) 连接到 USB 集线器的设备的物理设备对象的设备扩展。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种查找 USB 集线器 FDO 的设备扩展地址的方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
```

在上面的输出中，可以看到建议的命令 **！ devstack ffffe00002320050**。 输入此命令：

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

在上面的输出中，可以看到集线器的 FDO 的设备扩展的地址是 `ffffe000023201a0` 。

现在，将设备扩展的地址传递给 **！ usbkd. usbhubext** 命令。

```dbgcmd
0: kd> !usbkd.usbhubext ffffe000023201a0

FDO ffffe00002320050 PDO ffffe0000213c050 HubNumber# 3
dt USBHUB!_DEVICE_EXTENSION_HUB ffffe000023201a0
!usbhublog ffffe000023201a0
RemoveLock ffffe00002320668
FdoFlags ffffe00002320ba0

CurrentPowerIrp: System (0000000000000000) Device (0000000000000000)

ObjReferenceList: !usblist ffffe00002320b70, RL 
ExceptionList: !usblist ffffe00002321498, EL [Empty]
DmTimerListHead: !usblist ffffe00002321040, TL [Empty]
PdoRemovedListHead: !usblist ffffe00002321478, PL [Empty]
PdoPresentListHead: !usblist ffffe00002321468, PL 
WorkItemListHead: !usblist ffffe00002320c80, WI [Empty]
SshBusyListHead: !usblist ffffe00002320dc0, BL 


## PnP FUNC HISTORY (latest at bottom)

01. IRP_MN_QUERY_DEVICE_RELATIONS
...
## POWER FUNC HISTORY (latest at bottom)

01. IRP_MN_QUERY_POWER    - PowerSystemHibernate
...

## HARD RESET STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. HRE_Pause                       HReset_WaitReady                        HReset_Paused                           
...

## PNP STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. Ev_SYSTEM_POWER                 FDO_WaitPnpStop                         FDO_WaitPnpStop                         
...

## POWER STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. Ev_SET_POWER_S0                 FdoSx_Dx                                FdoWaitS0IoComplete_Dx                  
...

## BUS STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. BE_BusSuspend                   BS_BusPause                             BS_BusSuspend                           
...

SSH_EnabledStatus: [SSH_ENABLED_VIA_POWER_POLICY]

## SSH STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. SSH_Event_ResumeHubComplete     SSH_State_HubPendingResume              SSH_State_HubActive                     
...

## PORT DATA

PortData 1: !port2_info ffffe000021bf000 Port State = PS_WAIT_CONNECT PortChangeLock: 0, Pcq_State: Pcq_Run_Idle             
     PDO 0000000000000000 
...
```

下面是查找连接到 USB 集线器的设备的 PDO 的设备扩展地址的一种方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        Port 1: !port2_info ffffe000021bf000 
        Port 2: !port2_info ffffe000021bfb40 
        Port 3: !port2_info ffffe000021c0680 !devstack ffffe00007c882a0
```

在上面的输出中，可以看到建议的命令 **！ devstack ffffe00007c882a0**。 输入此命令：

```dbgcmd
0: kd> !kdexts.devstack ffffe00007c882a0

  !DevObj           !DrvObj            !DevExt           ObjectName
  ffffe00006ce2260  \Driver\USBSTOR    ffffe00006ce23b0  00000070
> ffffe00007c882a0  \Driver\usbhub     ffffe00007c883f0  USBPDO-4
...
```

在上面的输出中，可以看到设备的 PDO 的设备扩展地址是 `ffffe00007c883f0` 。

现在，将设备扩展的地址传递给 [**！ usbhcdpnp**](-usbkd-usbhcdpnp.md) 命令。

```dbgcmd
0: kd> !usbkd.usbhubext ffffe00007c883f0

dt USBHUB!_DEVICE_EXTENSION_PDO ffffe00007c883f0
PARENT HUB: FDO ffffe00002320050 !hub2_info ffffe000023201a0
!usbhubinfo ffffe00002320050
PORT NUMBER : 3
IoList: !usblist ffffe00007c888b0, IO 
LatchList: !usblist ffffe00007c888e0, LA 

## PnP ID's

DeviceId:USB\VID_0781&PID_5530  
HardwareId:USB\VID_0781&PID_5530&REV_0100USB\VID_0781&PID_5530  
CompatibleId:USB\Class_08&SubClass_06&Prot_50USB\Class_08&SubClass_06USB\Class_08  
SerialNumberId:20052444100A47F319CB  
UniqueId:3  
ProductId:Cruzer  

## Pnp Func History (latest at bottom)

01. IRP_MN_QUERY_BUS_INFORMATION
...

## Power Func History (latest at bottom)


## PNP STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. (6)                            (0)                                    PDO_WaitPnpStart                        
02. Ev_PDO_IRP_MN_START             PDO_WaitPnpStart                        PDO_WaitPnpStop                         

## POWER STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

    [EMPTY]

## HARDWARE STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

01. PdoEv_CreatePdo                 (0)                                    Pdo_Created                             
02. PdoEv_RegisterPdo               Pdo_Created                             Pdo_HwPresent                           
03. PdoEv_QBR                       Pdo_HwPresent                           Pdo_PnpRefHwPresent                     

## IDLE STATE HISTORY (latest at bottom)

##     EVENT                           STATE                                   NEXT

    [EMPTY]
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

