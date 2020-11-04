---
title: usb3kd.xhci_resourceusage
description: Usb3kd.xhci_resourceusage 扩展显示 USB 3.0 主机控制器使用的资源。
ms.assetid: 6AAB64D6-3CDA-4BA2-BBA8-F2F5AD1DBB6F
keywords:
- usb3kd.xhci_resourceusage Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_resourceusage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 15431f2261a6266a4672d9f24874bcbf15d5d0f6
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349723"
---
# <a name="usb3kdxhci_resourceusage"></a>！ usb3kd. xhci \_ resourceusage


[**！ Usb3kd. xhci \_ resourceusage**](-usb3kd-device-info.md)扩展显示 USB 3.0 主机控制器使用的资源。

```dbgcmd
!usb3kd.xhci_resourceusage DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
主机控制器的功能设备对象的设备扩展的地址 (FDO) 。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

Output **！ xhci \_ resourceusage** 命令基于 USB 3.0 主机控制器驱动程序所维护的数据结构 ( # A0) 。 有关 usb 3.0 主机控制器驱动程序和 USB 堆栈中其他驱动程序的详细信息，请参阅 [Windows 中的 usb 主机端驱动程序](../usbcon/usb-3-0-driver-stack-architecture.md)。

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
    !xhci_registers 0xfffffa800536e2d0
    !xhci_commandring 0xfffffa800536e2d0 (No commands are pending)
    !xhci_deviceslots 0xfffffa800536e2d0
    !xhci_eventring 0xfffffa800536e2d0
    !xhci_resourceusage 0xfffffa800536e2d0
    ...
```

现在可以将设备扩展的地址传递给 **！ xhci \_ resourceusage** 命令。

```dbgcmd
 3: kd> !xhci_resourceusage 0xfffffa800536e2d0

## Dumping CommonBuffer Resources
------------------------------
    dt USBXHCI!_COMMON_BUFFER_DATA 0xfffffa80059a5920
    DmaEnabler:!wdfdmaenabler 0x57ffa65a9c8

    CommonBuffers Large: Total 9 Available 2 Used 7 TotalBytes 36864
        [ 1] dt _TRACKING_DATA 0xfffffa80059a6768 VA 0xfffffa8005370000 LA 0x117170000 ...
        [ 2] dt _TRACKING_DATA 0xfffffa80059a4768 VA 0xfffffa8005373000 LA 0x117173000 ...
        ...
    CommonBuffers Small: Total 32 Available 8 Used 24 TotalBytes 16384
        [ 1] dt _TRACKING_DATA 0xfffffa80059a2798 VA 0xfffffa8005aeb000 LA 0x1168eb000 ...
        [ 2] dt _TRACKING_DATA 0xfffffa80059a27e8 VA 0xfffffa8005aeb200 LA 0x1168eb200 ...
        ...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

