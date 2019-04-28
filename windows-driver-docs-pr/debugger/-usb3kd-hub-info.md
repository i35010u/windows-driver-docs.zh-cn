---
title: usb3kd.hub_info
description: Usb3kd.device_info 命令在 USB 3.0 树中显示有关集线器的信息。
ms.assetid: B46B48C1-C14A-410D-9C34-F8AB1640682C
keywords:
- usb3kd.hub_info Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.hub_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 399a35aeaee39f782bc7e0b1fc19ac62c91d2d9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338764"
---
# <a name="usb3kdhubinfo"></a>!usb3kd.hub\_info


[ **！ Usb3kd.device\_信息**](-usb3kd-device-info.md)命令显示有关中的集线器信息[USB 3.0 树](usb-3-extensions.md#usb-3-tree)。

```dbgcmd
!usb3kd.hub_info DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
适用于中心的功能的设备对象 (FDO) 的设备扩展的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="examples"></a>示例
--------

若要获取设备扩展的地址，请查看的输出[ **！ usb\_树**](-usb3kd-usb-tree.md)命令。 在以下示例中，适用于根中心的设备扩展的地址是 0xfffffa8005ad92d0。

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------
Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId 0x1033 ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
        !port_info 0xfffffa8005a5ca80 !device_info 0xfffffa8005b410c0 Desc: <none> Speed: High
        ...
```

现在可以将传递到设备扩展的地址 **！ 中心\_信息**命令。

```dbgcmd
3: kd> !hub_info fffffa8005ad92d0 

## Dumping HUB Information fffffa8005ad92d0
----------------------------------------
dt USBHUB3!_HUB_FDO_CONTEXT 0xfffffa8005ad92d0
!rcdrlogdump usbhub3 -a 0xfffffa8005ad8010
Capabilities: Initialized, Configured, HasOverCurrentProtection, ...

Total number of ports: 4, HUB depth is 0
Number of 3.0 ports: 2 (Range 1 - 2)
Number of 2.0 ports: 2 (Range 3 - 4)

Descriptors:
    dt _USB_HUB_DESCRIPTOR 0xfffffa8005ad9728
    dt _USB_30_HUB_DESCRIPTOR 0xfffffa8005ad9728
    dt _USB_DEVICE_DESCRIPTOR 0xfffffa8005ad92d0
    dt _USB_CONFIGURATION_DESCRIPTOR 0xfffffa8005ad9770

List of PortContext: 4
    [1] !port_info 0xfffffa8005a5ca80    !device_info 0xfffffa8005b410c0
            Last Port Status(2.0): Connected Enabled Powered HighSpeedDeviceAttached
            Last Port Change: <none>
            Current Port(2.0) State: ConnectedEnabled.WaitingForPortChangeEvent
            Current Device State: ConfiguredInD0
    ...

Current Hub State: ConfiguredWithIntTransfer

Hub State History: <Event> NewState (<Operation>(),..) :

    [43] <OperationSuccess> ConfiguredWithIntTransfer 
    ...
Hub Event History:
    [ 0] PortEnableInterruptTransfer
    ...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!usb3kd.hub\_info\_from\_fdo**](-usb3kd-hub-info-from-fdo.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






