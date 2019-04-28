---
title: usb3kd.xhci_registers
description: Usb3kd.xhci_registers 扩展显示寄存器的 USB 3.0 主控制器。
ms.assetid: C695C23D-B617-4D1E-87F8-62CF99426CA3
keywords:
- usb3kd.xhci_registers Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_registers
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 47fdb22af1a2a6e18a908bce158f9c2619e407b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335630"
---
# <a name="usb3kdxhciregisters"></a>!usb3kd.xhci\_registers


[ **！ Usb3kd.xhci\_注册**](-usb3kd-device-info.md)扩展显示寄存器的 USB 3.0 主控制器。

```dbgcmd
!usb3kd.xhci_registers DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
适用于主机控制器的功能的设备对象 (FDO) 的设备扩展的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

输出 **！ xhci\_注册**命令基于 USB 3.0 主机控制器驱动程序 (UsbXhci.sys) 维护的数据结构。 有关 USB 3.0 主机控制器驱动程序和 USB 堆栈中的其他驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。

<a name="examples"></a>示例
--------

若要获取设备扩展的地址，请查看的输出[ **！ xhci\_dumpall** ](-usb3kd-xhci-dumpall.md)命令。 在以下示例中，设备扩展的地址是 0xfffffa800536e2d0。

```dbgcmd
3: kd> !xhci_dumpall

## Dumping all the XHCI controllers - DrvObj 0xfffffa80053072f0
------------------------------------------------------------
1)  ... - PCI: VendorId ... DeviceId ... RevisionId ... Firmware ...

    dt USBXHCI!_CONTROLLER_DATA 0xfffffa80052f20c0
    !rcdrlogdump USBXHCI -a 0xfffffa8005068520
    !rcdrlogdump USBXHCI -a 0xfffffa8004e8b9a0 (rundown)
    !wdfdevice 0x57ffac91fd8
    !xhci_capability 0xfffffa800536e2d0
    !xhci_registers 0xfffffa800536e2d0
    ...
```

现在可以将传递到设备扩展的地址 **！ xhci\_注册**命令。

```dbgcmd
3: kd> !xhci_registers 0xfffffa800536e2d0

## Dumping controller registers
----------------------------

    dt USBXHCI!_OPERATIONAL_REGISTERS 0xfffff880046a8020

    DeviceContextBaseAddressArrayPointer: 00000001168b9000

    Command Registers
    -----------------
        RunStopBit: 1
        HostControllerReset: 0
        ...

    Status Registers
    ----------------
        HcHalted: 0
        HostSystemError: 0
        ...

    commandRingControl Registers
    ----------------------------
        RingCycleState: 0
        CommandStop: 0
        ...
    Runtime Registers
    -----------------
        dt USBXHCI!_RUNTIME_REGISTERS 0xfffff880046a8600
        MicroFrameIndex: 0x3f7a

        dt -ba8 USBXHCI!_INTERRUPTER_REGISTER_SET 0xfffff880046a8620

    RootPort Registers
    ------------------
        dt -a4 -r2 USBXHCI!_PORT_REGISTER_SET 0xfffff880046a8420
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






