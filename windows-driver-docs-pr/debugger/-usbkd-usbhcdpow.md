---
title: usbkd.usbhcdpow
description: Usbkd.usbhcdpow 命令显示 USB 主控制器或根集线器的电源状态历史记录。
ms.assetid: 49D803E3-0D65-48D4-98C5-BFE4DB2C2985
keywords:
- usbkd.usbhcdpow Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpow
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29b6d960aa7e9a448bb44c68fb104d9962205766
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335572"
---
# <a name="usbkdusbhcdpow"></a>!usbkd.usbhcdpow


**！ Usbkd.usbhcdpow**命令显示 USB 主控制器或根集线器的电源状态历史记录。

```dbgcmd
!usbkd.usbhcdpow DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
其中一个以下地址：

-   USB 主控制器的功能的设备对象 (FDO) 设备扩展。
-   物理设备对象 (PDO) USB 根集线器设备扩展。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的 EHCI 主机控制器 FDO 设备扩展的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ ehci\_信息 ffffe00001ca11a0**。

现在将传递到设备扩展的地址 **！ usbhcdpow**命令。

```dbgcmd
0: kd> !usbkd.usbhcdpow ffffe00001ca11a0

dt USBPORT!_FDO_EXTENSION ffffe00001ca15a0

## State History (latest at bottom)

##      EVENT                              STATE                              NEXT

[00] FdoPwrEv_D0_DoSetD0_2              FdoPwr_D0_WaitWorker2              FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[01] FdoPwrEv_SyncUsb2_DoChirp          FdoPwr_D0_WaitSyncUsb2             FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[02] FdoPwrEv_Rh_SetPowerSys            FdoPwr_D0_WaitSyncUsb2             FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[03] FdoPwrEv_Rh_SetD0                  FdoPwr_D0_WaitSyncUsb2             FdoPwr_D0_WaitSyncUsb2               dt:0 ms
[04] FdoPwrEv_SyncUsb2_Complete         FdoPwr_D0_WaitSyncUsb2             FdoPwr_WaitSx                        dt:50 ms
[05] FdoPwrEv_Rh_Wake                   FdoPwr_WaitSx                      FdoPwr_WaitSx                        dt:3412 ms
[06] FdoPwrEv_Rh_Wake                   FdoPwr_WaitSx                      FdoPwr_WaitSx                        dt:283872 ms
[07] FdoPwrEv_Rh_Wake                   FdoPwr_WaitSx                      FdoPwr_WaitSx                        dt:25481267 ms
```

下面是一种方法，若要查找的是 PDO 根中心的设备扩展的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        ...
```

在上面的输出中可以看到的地址显示为该命令的参数的根集线器 FDO **！ devstack ffffe00002320050**。 使用[ **！ devstack** ](-devstack.md)命令来查找对 PDO 和 PDO 设备扩展的地址。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

在上面的输出，您可以看到的是 PDO 根中心的设备扩展的地址是`ffffe0000213c1a0`。

现在将传递到设备扩展的地址 **！ usbhcdpow**命令。

```dbgcmd
0: kd> !usbkd.usbhcdpow ffffe0000213c1a0

dt USBPORT!_FDO_EXTENSION ffffe0000213c5a0

## State History (latest at bottom)

##      EVENT                              STATE                              NEXT

...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






