---
title: usb3kd.xhci_info
description: Usb3kd.xhci_info 扩展显示为单独的 USB 3.0 主控制器的所有 XHCI 命令。
ms.assetid: C3C3B379-4871-4293-9C35-B64F3A5E1348
keywords:
- usb3kd.xhci_info Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a2c15b15393d1eeca1045222e89884f00edf1feb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521486"
---
# <a name="usb3kdxhciinfo"></a>!usb3kd.xhci\_info


[ **！ Usb3kd.xhci\_信息**](-usb3kd-device-info.md)扩展显示为单独的 USB 3.0 主控制器的所有 XHCI 命令。

```dbgcmd
!usb3kd.xhci_info DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
适用于主机控制器的功能的设备对象 (FDO) 的设备扩展的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

输出 **！ usb3kd.xhci\_信息**命令基于 USB 3.0 主机控制器驱动程序 (UsbXhci.sys) 维护的数据结构。 有关 USB 3.0 主机控制器驱动程序和 USB 堆栈中的其他驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。

<a name="examples"></a>示例
--------

你可以将地址中的设备扩展[ **！ xhci\_dumpall** ](-usb3kd-xhci-dumpall.md)命令或使用不同的其他调试器命令。 例如， [ **！ devstack** ](-devstack.md)命令显示设备扩展的地址。 以下示例中，在主控制器 FDO 设备扩展的地址是 fffffa800536e2d0。

```dbgcmd
3: kd> !devnode 0 1 usbxhci
Dumping IopRootDeviceNode (= 0xfffffa8003609cc0)
DevNode 0xfffffa8003df3010 for PDO 0xfffffa8003dd5870
  InstancePath is "PCI\VEN_...
  ServiceName is "USBXHCI"
  ...

3: kd> !devstack 0xfffffa8003dd5870
  !DevObj   !DrvObj            !DevExt   ObjectName
  fffffa800534b060  \Driver\USBXHCI    fffffa800536e2d0  USBFDO-3
  fffffa8003db5790  \Driver\ACPI       fffffa8003701cb0  
> fffffa8003dd5870  \Driver\pci        fffffa8003dd59c0  NTPNP_PCI0020
...
```

现在可以将传递到设备扩展的地址 **！ xhci\_信息**命令。

```dbgcmd
3: kd> !xhci_info 0xfffffa80`0536e2d0

## Dumping XHCI controller commands - DeviceExtension 0xfffffa800536e2d0
------------------------------------------------------------
 ... - PCI: VendorId ... DeviceId ... RevisionId ... Firmware ...

    dt USBXHCI!_CONTROLLER_DATA 0xfffffa80052f20c0
    !rcdrlogdump USBXHCI -a 0xfffffa8005068520
    !rcdrlogdump USBXHCI -a 0xfffffa8004e8b9a0 (rundown)
    !wdfdevice 0x57ffac91fd8
    !xhci_capability 0xfffffa800536e2d0
    !xhci_registers 0xfffffa800536e2d0
    !xhci_commandring 0xfffffa800536e2d0 (No commands are pending)
    !xhci_deviceslots 0xfffffa800536e2d0
    !xhci_eventring 0xfffffa800536e2d0
    !xhci_resourceusage 0xfffffa800536e2d0
    !pci 100 0x30 0x0 0x0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






