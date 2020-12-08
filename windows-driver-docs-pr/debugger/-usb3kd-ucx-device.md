---
title: usb3kd.ucx_device
description: Usb3kd.ucx_device 扩展在 USB 3.0 树中显示有关 USB 设备的信息。 该显示基于 UcxVersion.sys 维护的数据结构。
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
ms.openlocfilehash: 6b19258f9e675be7e1ca863548343da846566a97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814047"
---
# <a name="usb3kducx_device"></a>！ usb3kd ucx \_ 设备


[**！ Usb3kd ucx \_ 设备**](-usb3kd-device-info.md)扩展在 [usb 3.0 树](usb-3-extensions.md#usb-3-tree)中显示有关 usb 设备的信息。 此显示基于 USB 主机控制器扩展驱动程序所维护的数据结构，*(Ucx .sys) 。*

```dbgcmd
!usb3kd.ucx_device UcxUsbDevicePrivContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UcxUsbDevicePrivContext______"></span><span id="_______ucxusbdeviceprivcontext______"></span><span id="_______UCXUSBDEVICEPRIVCONTEXT______"></span>*UcxUsbDevicePrivContext*   
\_表示设备的 UCXUSBDEVICE \_ PRIVCONTEXT 结构的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

USB 主机控制器扩展驱动程序 (Ucx *版本*.sys) 提供 usb 3.0 集线器驱动程序与 usb 3.0 主机控制器驱动程序之间的抽象层。 扩展驱动程序具有其自己的主机控制器、设备和终结点的表示形式。 输出 [**！ ucx \_ device**](-usb3kd-device-info.md) 命令基于扩展驱动程序所维护的数据结构。 有关 USB 主机控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序的详细信息，请参阅 [Usb 驱动程序堆栈体系结构](/windows-hardware/drivers/ddi/index)。

**！ ucx \_ 设备** 和 [**！设备 \_ 信息**](-usb3kd-device-info.md) 都显示设备的相关信息，但显示的信息不同。 **！ Ucx \_ 设备** 的输出来自 usb 主机控制器扩展驱动程序的位置，而 **！设备 \_ 信息** 的输出来自 usb 3.0 集线器驱动程序的视图。 例如， **！ ucx \_ 设备** 输出包含有关终结点的信息，而 **！设备 \_ 信息** 输出包含有关配置和接口描述符的信息。

<a name="examples"></a>示例
--------

若要获取 UCX USB 设备专用上下文的地址，请查看 [**！ UCX \_ controller \_ list**](-usb3kd-ucx-controller-list.md) 命令的输出。 在下面的示例中，第二个设备的专用上下文地址为0xfffffa8005bd9680。

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

现在可以将 UCX USB private 上下文的地址传递给 **！ UCX \_ 设备** 命令。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ usb3kd ucx \_ 控制器 \_ 列表**](-usb3kd-ucx-controller-list.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

