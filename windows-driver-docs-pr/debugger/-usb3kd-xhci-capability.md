---
title: usb3kd.xhci_capability
description: Usb3kd.xhci_capability 扩展显示 USB 3.0 主机控制器的功能。
keywords:
- usb3kd.xhci_capability Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_capability
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ac3b5122bd3c8f71f776e98238dcd4cf8385867e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832547"
---
# <a name="usb3kdxhci_capability"></a>！ usb3kd xhci \_ 功能


[**！ Usb3kd xhci \_ 功能**](-usb3kd-device-info.md)扩展显示 USB 3.0 主机控制器的功能。

```dbgcmd
!usb3kd.xhci_capability DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
主机控制器的功能设备对象的设备扩展的地址 (FDO) 。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

输出 [**！ xhci \_ 功能**](-usb3kd-device-info.md) 命令基于 USB 3.0 主机控制器驱动程序所维护的数据结构 ( # A0) 。 有关 usb 3.0 主机控制器驱动程序和 USB stack 中其他驱动程序的详细信息，请参阅 [Usb 驱动程序堆栈体系结构](/windows-hardware/drivers/ddi/index)。

<a name="examples"></a>示例
--------

若要获取设备扩展的地址，请查看 [**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md) 命令的输出。 在以下示例中，设备扩展的地址为0xfffffa800536e2d0。

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
    ...
```

现在可以将设备扩展的地址传递到 **！ xhci \_ 功能** 命令。

```dbgcmd
3: kd> !xhci_capability 0xfffffa800536e2d0

## Controller Capabilities
-----------------------
    dt USBXHCI!_REGISTER_DATA 0xfffffa8005362c00
    dt USBXHCI!_CAPABILITY_REGISTERS 0xfffff880046a8000
    MajorRevision.MinorRevision = 0.96
    Device Slots: 32
    Interrupters: 8
    Ports: 4
    IsochSchedulingThreshold: 1
    EventRingSegmentTableMax: 1 (2^ERST = 2)
    ScratchpadRestore: OFF
    MaxScratchpadBuffers: 0
    U1DeviceExitLatency: 0
    U2DeviceExitLatency: 0
    AddressingCapability: 64 bit
    BwNegotiationCapability: ON
    ContextSize: 32 bytes
    PortPowerControl: ON
    PortIndicators: OFF
    LightHCResetCapability: OFF
    LatencyToleranceMessagingCapability: ON
    NoSecondarySidSupport: TRUE
    MaximumPrimaryStreamArraySize = 4 ( 2^(MaxPSASize+1) = 32 )
    XhciExtendedCapabilities:
        [1] USB_LEGACY_SUPPORT: dt _USBLEGSUP 0xfffff880046a8500
        [2] Supported Protocol 0xfffff880046a8510, Version 3.0, Offset 1, Count 2, HighSpeedOnly OFF, IntegratedHub OFF, HardwareLPM OFF
        [3] Supported Protocol 0xfffff880046a8520, Version 2.0, Offset 3, Count 2, HighSpeedOnly OFF, IntegratedHub OFF, HardwareLPM OFF

## Software Supported Capabilities
-------------------------------
    DeviceSlots: 32
    Interrupters: 1
    Ports: 4
    MaxEventRingSegments: 2
    U1DeviceExitLatency: 0
    U2DeviceExitLatency: 0
    DeviceFlags:
        IgnoreBiosHandoffFailure
        SetLinkTrbChainBit
        UseSingleInterrupter
        DisableIdlePowerManagement
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

