---
title: usbkd.usbhcdpow
description: Usbkd. usbhcdpow 命令显示 USB 主机控制器或根集线器的电源状态历史记录。
keywords:
- usbkd usbhcdpow Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpow
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 04c88818ac94154b80e3217b5747e00d6d3a779d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818673"
---
# <a name="usbkdusbhcdpow"></a>!usbkd.usbhcdpow


**！ Usbkd. usbhcdpow** 命令显示 USB 主机控制器或根集线器的电源状态历史记录。

```dbgcmd
!usbkd.usbhcdpow DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
以下项之一的地址：

-   功能设备对象的设备扩展 (USB 主机控制器的 FDO) 。
-    (PDO) USB 根集线器的物理设备对象的设备扩展。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种查找 EHCI 主机控制器的 FDO 的设备扩展地址的方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

在上面的输出中，FDO 的设备扩展的地址显示为 [DML](debugger-markup-language-commands.md) 命令 **！ ehci \_ info ffffe00001ca11a0** 的参数。

现在，将设备扩展的地址传递给 **！ usbhcdpow** 命令。

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

下面是一种查找根集线器 PDO 的设备扩展地址的方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        ...
```

在上面的输出中，可以看到根集线器的 FDO 地址，该地址显示为命令 **！ devstack ffffe00002320050** 的参数。 使用 [**！ devstack**](-devstack.md) 命令查找 pdo 的地址和 pdo 设备扩展。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

在上面的输出中，可以看到根集线器的 PDO 的设备扩展地址是 `ffffe0000213c1a0` 。

现在，将设备扩展的地址传递给 **！ usbhcdpow** 命令。

```dbgcmd
0: kd> !usbkd.usbhcdpow ffffe0000213c1a0

dt USBPORT!_FDO_EXTENSION ffffe0000213c5a0

## State History (latest at bottom)

##      EVENT                              STATE                              NEXT

...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

