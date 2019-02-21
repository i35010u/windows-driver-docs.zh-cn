---
title: usb3kd.device_info_from_pdo
description: Usb3kd.device_info_from_pdo 命令在 USB 3.0 树中显示有关 USB 设备的信息。
ms.assetid: 74FD68E6-78DF-452F-80C2-91A37877DE52
keywords:
- usb3kd.device_info_from_pdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.device_info_from_pdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 48e5d06b96c0dc41678c9fc30f8c11a7e2d71016
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555657"
---
# <a name="usb3kddeviceinfofrompdo"></a>!usb3kd.device\_info\_from\_pdo


**！ Usb3kd.device\_信息\_从\_pdo**命令显示有关 USB 设备中的信息[USB 3.0 树](usb-3-extensions.md#usb-3-tree)。

```dbgcmd
!usb3kd.device_info_from_pdo DeviceObject
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
USB 设备或中心的物理设备对象 (PDO) 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ 设备\_info\_从\_pdo**并[ **！ ucx\_设备**](-usb3kd-ucx-device.md)两者都显示有关设备的信息，但信息显示与不同。 输出 **！ 设备\_信息\_从\_pdo** USB 3.0 集线器驱动程序，point of view 和的输出来自 **！ ucx\_设备**来自角度来看的 USB 主控制器扩展驱动程序。 例如， **！ 设备\_信息\_从\_pdo**输出包含有关配置和接口描述符并 **！ ucx\_设备**输出包括终结点的信息。

<a name="examples"></a>示例
--------

可以从的输出中获取的地址的 PDO [ **！ usb\_树**](-usb3kd-usb-tree.md)或使用不同的其他调试器命令。 例如， [ **！ devnode** ](-devnode.md)命令显示 PDOs 的地址。 在以下示例中，USBSTOR 设备节点是 USBHUB3 节点的直接子级。 PDO USBSTOR 节点的地址是 0xfffffa80059c3800。

```dbgcmd
3: kd> !devnode 0 1 usbhub3

Dumping IopRootDeviceNode (= 0xfffffa8003609cc0)
DevNode 0xfffffa8005981730 for PDO 0xfffffa8004ffc550
  InstancePath is "USB\ROOT_HUB30\5&11db9684&0&0"
  ServiceName is "USBHUB3"
  State = DeviceNodeStarted (0x308)
  Previous State = DeviceNodeEnumerateCompletion (0x30d)

  DevNode 0xfffffa8005a546a0 for PDO 0xfffffa80059c3800
    InstancePath is "USB\VID_125F&PID_312A\09021000000000000342192873"
    ServiceName is "USBSTOR"
    State = DeviceNodeStarted (0x308)
    Previous State = DeviceNodeEnumerateCompletion (0x30d)

    DevNode 0xfffffa8005a09730 for PDO 0xfffffa8005b3a650
      InstancePath is "USBSTOR\Disk&Ven ...
      ServiceName is "disk"
      State = DeviceNodeStarted (0x308)
      Previous State = DeviceNodeEnumerateCompletion (0x30d)
```

现在可以将传递给 PDO 的地址 **！ usb3kd.device\_信息\_从\_pdo**命令。

```dbgcmd
3: kd> !device_info_from_pdo 0xfffffa80059c3800

## Dumping Device Information fffffa80059c3800
-------------------------------------------
!devobj 0xfffffa8004ffc550 (Root HUB)
!device_info 0xfffffa8005abd0c0 (dt usbhub3!_DEVICE_CONTEXT 0xfffffa8005abd0c0)
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
ProductId: ...
DeviceDescriptor: VID ...

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

下面的示例显示了一些的输出[ **！ usb\_树**](-usb3kd-usb-tree.md)命令。 您所见的其中一个子设备节点 PDO 的地址作为参数[ **！ devstack** ](-devstack.md)命令。 (**!devstack fffffa80059c3800**)

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------

Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
        !port_info 0xfffffa8005a5ca80 !device_info 0xfffffa8005b410c0 Desc: <none> Speed: High
        ...
## Enumerated Device List
----------------------
...

2) !device_info 0xfffffa8005abd0c0, !devstack fffffa80059c3800
    Current Device State: ConfiguredInD0
    Desc: ... Flash Drive
    USB\VID_...
    !ucx_device 0xfffffa8005992840 !xhci_deviceslots 0xfffffa80051d1940 1
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!usb3kd.device\_info**](-usb3kd-device-info.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






