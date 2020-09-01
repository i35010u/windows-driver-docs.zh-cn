---
title: usb3kd hub_info
description: Device_info usb3kd 命令显示有关 USB 3.0 树中的集线器的信息。
ms.assetid: B46B48C1-C14A-410D-9C34-F8AB1640682C
keywords:
- usb3kd hub_info Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.hub_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b414af24ccb233911587e186315384c76ab40ff
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206601"
---
# <a name="usb3kdhub_info"></a>！ usb3kd \_ 信息


[**！ Usb3kd \_ info**](-usb3kd-device-info.md)命令显示有关[USB 3.0 树](usb-3-extensions.md#usb-3-tree)中的集线器的信息。

```dbgcmd
!usb3kd.hub_info DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
中心功能设备对象的设备扩展的地址 (FDO) 。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="examples"></a>示例
--------

若要获取设备扩展的地址，请查看 [**！ usb \_ 树**](-usb3kd-usb-tree.md) 命令的输出。 在以下示例中，根集线器的设备扩展地址为0xfffffa8005ad92d0。

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

现在可以将设备扩展的地址传递到 **！ hub \_ 信息** 命令。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ usb3kd \_ \_ fdo 中的信息 \_**](-usb3kd-hub-info-from-fdo.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

