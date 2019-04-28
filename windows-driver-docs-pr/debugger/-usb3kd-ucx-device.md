---
title: usb3kd.ucx_device
description: Usb3kd.ucx_device 扩展在 USB 3.0 树中显示有关 USB 设备的信息。 显示基于由 UcxVersion.sys 维护的数据结构。
ms.assetid: 7AC3DBBF-1D62-492E-B46E-C193579DE1E3
keywords:
- usb3kd.ucx_device Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_device
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e531175c38ab20fd474c7f7bef18d2f3ca26e371
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335653"
---
# <a name="usb3kducxdevice"></a>！ usb3kd.ucx\_设备


[ **！ Usb3kd.ucx\_设备**](-usb3kd-device-info.md)扩展显示有关 USB 设备中的信息[USB 3.0 树](usb-3-extensions.md#usb-3-tree)。 显示基于 USB 主控制器扩展驱动程序所维护的数据结构 (Ucx*版本*.sys)。

```dbgcmd
!usb3kd.ucx_device UcxUsbDevicePrivContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UcxUsbDevicePrivContext______"></span><span id="_______ucxusbdeviceprivcontext______"></span><span id="_______UCXUSBDEVICEPRIVCONTEXT______"></span> *UcxUsbDevicePrivContext*   
地址\_UCXUSBDEVICE\_PRIVCONTEXT 结构，它表示该设备。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

USB 主控制器扩展驱动程序 (Ucx*版本*.sys) 提供的 USB 3.0 集线器驱动程序和 USB 3.0 主机之间的抽象层，控制器驱动程序。 扩展驱动程序具有其自己的主机控制器、 设备和终结点的表示形式。 输出[ **！ ucx\_设备**](-usb3kd-device-info.md)命令基于由扩展驱动程序维护的数据结构。 有关 USB 主控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://msdn.microsoft.com/library/windows/hardware/hh406256)。

**！ ucx\_设备**并[ **！ 设备\_信息**](-usb3kd-device-info.md)两者都显示有关设备的信息，但显示的信息不同。 输出 **！ ucx\_设备**是从 USB 主控制器扩展驱动程序的 point of view 和输出 **！ 设备\_信息**是从 USB 3.0 集线器的角度驱动程序。 例如， **！ ucx\_设备**输出包含有关终结点，并且 **！ 设备\_信息**输出包含有关配置和接口描述符。

<a name="examples"></a>示例
--------

若要获取的地址 UCX USB 设备专用上下文，请查看的输出[ **！ ucx\_控制器\_列表**](-usb3kd-ucx-controller-list.md)命令。 在以下示例中，第二个设备的专用上下文的地址是 0xfffffa8005bd9680。

```dbgcmd
3: 3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        ...
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        ...
```

现在可以将传递到 UCX USB 专用上下文的地址 **！ ucx\_设备**命令。

```dbgcmd
3: kd> !ucx_device 0xfffffa8005bd9680

## Dumping Ucx USB Device Information fffffa8005bd9680
---------------------------------------------------
dt ucx01000!_UCXUSBDEVICE_PRIVCONTEXT 0xfffffa8005bd9680
!ucx_controller 0xfffffa80052da050
ParentHub: !wdfhandle 0x57ffacbce78
DefaultEndpoint: !ucx_endpoint 0xfffffa8005be0550
ListOfEndpionts:
    .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
    .!ucx_endpoint 0xfffffa8003686820 [Blk In ], UcxEndpointStateEnabled
    .!ucx_endpoint 0xfffffa8005be0550 [Control], UcxEndpointStateEnabled
    .!ucx_endpoint 0xfffffa8003695580 [Blk In ], UcxEndpointStateStale
    .!ucx_endpoint 0xfffffa80036a20c0 [Blk Out], UcxEndpointStateStale

EventCallbacks:
    EvtUsbDeviceEndpointsConfigure: (0xfffff880044d1164) USBXHCI!UsbDevice_UcxEvtEndpointsConfigure
    EvtUsbDeviceEnable: (0xfffff880044cffac) USBXHCI!UsbDevice_UcxEvtEnable
    EvtUsbDeviceDisable: (0xfffff880044d1cbc) USBXHCI!UsbDevice_UcxEvtDisable
    EvtUsbDeviceReset: (0xfffff880044d2178) USBXHCI!UsbDevice_UcxEvtReset
    EvtUsbDeviceAddress: (0xfffff880044d0934) USBXHCI!UsbDevice_UcxEvtAddress
    EvtUsbDeviceUpdate: (0xfffff880044d0c80) USBXHCI!UsbDevice_UcxEvtUpdate
    EvtUsbDeviceDefaultEndpointAdd: (0xfffff880044ede1c) USBXHCI!Endpoint_UcxEvtUsbDeviceDefaultEndpointAdd
    EvtUsbDeviceEndpointAdd: (0xfffff880044edfc8) USBXHCI!Endpoint_UcxEvtUsbDeviceEndpointAdd
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!usb3kd.ucx\_controller\_list**](-usb3kd-ucx-controller-list.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






