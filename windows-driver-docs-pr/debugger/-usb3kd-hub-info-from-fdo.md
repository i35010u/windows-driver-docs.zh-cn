---
title: usb3kd hub_info_from_fdo
description: Hub_info_from_fdo usb3kd 命令显示有关 USB 3.0 树中的集线器的信息。
ms.assetid: 07A1C3EC-76A9-49A5-8467-53FCE3667203
keywords:
- usb3kd hub_info_from_fdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.hub_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3f1251aa281e7c32a20b72cd89a6413819e15210
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209877"
---
# <a name="usb3kdhub_info_from_fdo"></a>！ usb3kd \_ \_ fdo 中的信息 \_


Fdo 命令中的 **！ \_ usb3kd \_ Info \_ ** 显示有关 [USB 3.0 树](usb-3-extensions.md#usb-3-tree)中的集线器的信息。

```dbgcmd
!usb3kd.hub_info_from_fdo DeviceObject
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span>*DeviceObject*   
功能设备对象的地址 (表示中心的 FDO) 。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="examples"></a>示例
--------

可以从 [**！ usb \_ 树**](-usb3kd-usb-tree.md) 的输出或其他各种调试器命令中获取 FDO 的地址。 例如， [**！ devstack**](-devstack.md) 命令显示 FDO 的地址。 在下面的示例中，FDO 的地址为 fffffa800597a660。

```dbgcmd
3: kd> !devnode 0 1 usbhub3
Dumping IopRootDeviceNode (= 0xfffffa8003609cc0)
DevNode 0xfffffa8005981730 for PDO 0xfffffa8004ffc550
...
3: kd> !devstack 0xfffffa8004ffc550
  !DevObj   !DrvObj            !DevExt   ObjectName
  fffffa800597a660  \Driver\USBHUB3    fffffa8005ad92d0  
> fffffa8004ffc550  \Driver\USBXHCI    fffffa8005251d00  USBPDO-0
...
```

现在，可以通过 FDO 命令将 FDO 的地址传递给 **！ usb3kd \_ 信息 \_ \_ ** 。

```dbgcmd
 3: kd> !hub_info_from_fdo fffffa800597a660

## Dumping HUB Information fffffa800597a660
----------------------------------------
dt USBHUB3!_HUB_FDO_CONTEXT 0xfffffa8005ad92d0
!rcdrlogdump usbhub3 -a 0xfffffa8005ad8010
Capabilities: Initialized, Configured, HasOverCurrentProtection, SelectiveSuspendSupportedByParentStack, CannotWakeOnConnect, NotArmedForWake

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

[**！ usb3kd \_ 信息**](-usb3kd-hub-info.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

