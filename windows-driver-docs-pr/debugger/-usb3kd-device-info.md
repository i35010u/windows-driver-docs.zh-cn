---
title: usb3kd.device_info
description: Usb3kd.device_info 命令显示有关 USB 3.0 树中 USB 设备的信息。
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
ms.openlocfilehash: 6e5aa791db9ad667abc44c23a652d992e78e093b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837011"
---
# <a name="usb3kddevice_info"></a>！ usb3kd \_ 信息


**！ Usb3kd \_ info** 命令显示有关 [USB 3.0 树](usb-3-extensions.md#usb-3-tree)中 usb 设备的信息。

```dbgcmd
!usb3kd.device_info DeviceContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceContext______"></span><span id="_______devicecontext______"></span><span id="_______DEVICECONTEXT______"></span>*DeviceContext*   
\_表示设备的设备 \_ 上下文结构的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！设备 \_ 信息** 和 [**！ ucx \_ 设备**](-usb3kd-ucx-device.md) 都显示设备的相关信息，但显示的信息不同。 **！设备 \_ 信息** 的输出来自 usb 3.0 集线器驱动程序的位置，而 **！ ucx \_ 设备** 的输出来自 usb 主机控制器扩展驱动程序的位置。 例如， **！设备 \_ 信息** 输出包含有关配置和接口描述符的信息， **！ ucx \_ 设备** 输出包含有关终结点的信息。

<a name="examples"></a>示例
--------

可以通过查看 [**！ usb \_ 树**](-usb3kd-usb-tree.md) 命令的输出来获取设备上下文结构的地址。 在下面的示例中，设备上下文结构的地址为0xfffffa8005abd0c0。

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

现在可以将设备上下文的地址传递到 **！设备 \_ 信息** 命令。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ usb3kd \_ \_ 来自 pdo 的设备 \_ 信息**](-usb3kd-device-info-from-pdo.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

