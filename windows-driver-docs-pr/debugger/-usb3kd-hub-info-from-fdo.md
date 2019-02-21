---
title: usb3kd.hub_info_from_fdo
description: Usb3kd.hub_info_from_fdo 命令在 USB 3.0 树中显示有关集线器的信息。
ms.assetid: 07A1C3EC-76A9-49A5-8467-53FCE3667203
keywords:
- usb3kd.hub_info_from_fdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.hub_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0932f332e22ec602b0860685b0ea443f711a5e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522018"
---
# <a name="usb3kdhubinfofromfdo"></a>!usb3kd.hub\_info\_from\_fdo


**！ Usb3kd.hub\_信息\_从\_fdo**命令显示有关中的集线器信息[USB 3.0 树](usb-3-extensions.md#usb-3-tree)。

```dbgcmd
!usb3kd.hub_info_from_fdo DeviceObject
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceObject______"></span><span id="_______deviceobject______"></span><span id="_______DEVICEOBJECT______"></span> *DeviceObject*   
表示集线器的功能的设备对象 (FDO) 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="examples"></a>示例
--------

可以从的输出中获取的地址 FDO [ **！ usb\_树**](-usb3kd-usb-tree.md)或使用不同的其他调试器命令。 例如， [ **！ devstack** ](-devstack.md)命令显示 FDO 的地址。 在以下示例中，FDO 的地址是 fffffa800597a660。

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

现在可以将传递到 FDO 的地址 **！ usb3kd.hub\_信息\_从\_fdo**命令。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!usb3kd.hub\_info**](-usb3kd-hub-info.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






