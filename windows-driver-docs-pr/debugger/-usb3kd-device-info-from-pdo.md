---
title: usb3kd device_info_from_pdo
description: Device_info_from_pdo usb3kd 命令在 USB 3.0 树中显示有关 USB 设备的信息。
ms.assetid: 74FD68E6-78DF-452F-80C2-91A37877DE52
keywords:
- usb3kd device_info_from_pdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.device_info_from_pdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e671d6247941c7ab38856586c9a821663870026
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216298"
---
# <a name="usb3kddevice_info_from_pdo"></a>！ usb3kd \_ \_ 来自 pdo 的设备 \_ 信息


** \_ \_ 来自 \_ pdo 的！ usb3kd 信息**命令显示有关[usb 3.0 树](usb-3-extensions.md#usb-3-tree)中 usb 设备的信息。

```dbgcmd
!usb3kd.device_info_from_pdo DeviceObject
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
USB 设备或集线器 (PDO) 的物理设备对象的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ \_ \_ 来自 \_ pdo** 和 [**！ ucx \_ 设备**](-usb3kd-ucx-device.md) 的设备信息均显示有关设备的信息，但显示的信息不同。 ** \_ \_ 来自 \_ pdo 的！设备信息**的输出来自于 usb 3.0 集线器驱动程序的观点， **！ ucx \_ 设备**的输出来自 usb 主机控制器扩展驱动程序的观点。 例如， ** \_ \_ 来自 \_ pdo 输出的！设备信息** 包含有关配置和接口描述符的信息， **！ ucx \_ 设备** 输出包含有关终结点的信息。

<a name="examples"></a>示例
--------

可以从 [**！ usb \_ 树**](-usb3kd-usb-tree.md) 的输出或其他各种调试器命令获取 PDO 的地址。 例如， [**！ devnode**](-devnode.md) 命令显示 PDOs 的地址。 在下面的示例中，USBSTOR 设备节点是 USBHUB3 节点的直接子节点。 USBSTOR 节点的 PDO 地址为0xfffffa80059c3800。

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

现在，可以通过 pdo 命令将 PDO 地址传递到 **！ usb3kd \_ info \_ \_ ** 。

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

下面的示例演示了 [**！ usb \_ 树**](-usb3kd-usb-tree.md) 命令的一些输出。 可以查看其中一个子设备节点的 PDO 地址作为 [**！ devstack**](-devstack.md) 命令的参数。  (**！ devstack fffffa80059c3800**) 

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ usb3kd \_ 信息**](-usb3kd-device-info.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

