---
title: usb3kd.device_info
description: Usb3kd.device_info 命令在 USB 3.0 树中显示有关 USB 设备的信息。
ms.assetid: BD6D1562-2606-42C1-9EE6-D38D93D685DE
keywords:
- usb3kd.device_info Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.device_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86f6872f33878d36433f939c75841de65a9fa4b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335664"
---
# <a name="usb3kddeviceinfo"></a>!usb3kd.device\_info


**！ Usb3kd.device\_信息**命令将显示有关 USB 设备中的信息[USB 3.0 树](usb-3-extensions.md#usb-3-tree)。

```dbgcmd
!usb3kd.device_info DeviceContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceContext______"></span><span id="_______devicecontext______"></span><span id="_______DEVICECONTEXT______"></span> *DeviceContext*   
地址\_设备\_上下文结构，它表示该设备。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ 设备\_info**并[ **！ ucx\_设备**](-usb3kd-ucx-device.md)两者都显示有关设备的信息，但显示的信息不同。 输出 **！ 设备\_信息**是从 USB 3.0 集线器驱动程序，point of view 和输出 **！ ucx\_设备**是从 USB 主机控制器扩展的角度驱动程序。 例如， **！ 设备\_信息**输出包含有关配置和接口描述符并 **！ ucx\_设备**输出包括下列相关信息终结点。

<a name="examples"></a>示例
--------

可以通过查看的输出中获取设备上下文结构的地址[ **！ usb\_树**](-usb3kd-usb-tree.md)命令。 在以下示例中，设备上下文结构的地址是 0xfffffa8005abd0c0。

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------

Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
    ...
## Enumerated Device List
----------------------
...

2) !device_info 0xfffffa8005abd0c0, !devstack fffffa80059c3800
    Current Device State: ConfiguredInD0
    Desc: ... USB Flash Drive
    ...
```

现在可以将传递到设备上下文的地址 **！ 设备\_信息**命令。

```dbgcmd
3: kd> !device_info 0xfffffa8005abd0c0

## Dumping Device Information fffffa8005abd0c0
-------------------------------------------
dt USBHUB3!_DEVICE_CONTEXT 0xfffffa8005abd0c0
dt USBHUB3!_HUB_PDO_CONTEXT 0xfffffa8005b118d0
!idle_info 0xfffffa8005b11920 (dt USBHUB3!_ISM_CONTEXT 0xfffffa8005b11920)
Parent !hub_info 0xfffffa8005ad92d0 (dt USBHUB3!_HUB_FDO_CONTEXT 0xfffffa8005ad92d0)
!port_info 0xfffffa8005abe0c0 (dt USBHUB3!_PORT_CONTEXT 0xfffffa8005abe0c0)
!ucx_device 0xfffffa8005992840 !xhci_deviceslots 0xfffffa80051d1940 1

LPMState: U1IsEnabledForUpStreamPort U2IsEnabledForUpStreamPort U1Timeout: 38, U2Timeout: 3
DeviceFlags: HasContainerId NoBOSContainerId Removable HasSerialNumber MsOsDescriptorNotSupported NoWakeUpSupport DeviceIsSuperSpeedCapable 
DeviceHackFlags: WillDisableOnSoftRemove SkipSetIsochDelay WillResetOnResumeS0 DisableOnSoftRemove 

Descriptors:
dt _USB_CONFIGURATION_DESCRIPTOR 0xfffffa80053f9250
dt _USB_INTERFACE_DESCRIPTOR 0xfffffa80053f9259
ProductId: ... Flash Drive
DeviceDescriptor: VID ... PID ... REV 0a00,  Class: (0)(0) BcdUsb: 0300

UcxRequest: !wdfrequest 0x57ffa662948, 
ControlRequest: !wdfrequest 0x57ffa667798, !irp 0xfffffa8005997650 !urb 0xfffffa8005abd1c0, NumberOfBytes 0
Device working at SuperSpeed
Current Device State: ConfiguredInD0

Device State History: <Event> NewState (<Operation>(),..) :

    [16] <Yes> ConfiguredInD0
    ...
Device Event History:
    [10] TransferSuccess
    ...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!usb3kd.device\_info\_from\_pdo**](-usb3kd-device-info-from-pdo.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






