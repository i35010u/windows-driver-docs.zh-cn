---
title: usb3kd ucx_endpoint
description: Ucx_endpoint usb3kd 命令显示有关 USB 3.0 树中 USB 设备上的终结点的信息。 该显示基于 UcxVersion.sys 维护的数据。
ms.assetid: 37667665-ACA1-48D3-B79E-5B9BBD689034
keywords:
- usb3kd ucx_endpoint Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_endpoint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00e2d36f9c5beb7de5ec61c71b01ba7473125eca
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217423"
---
# <a name="usb3kducx_endpoint"></a>！ usb3kd ucx \_ 终结点


[**！ Usb3kd ucx \_ 终结点**](-usb3kd-device-info.md)命令显示 usb [3.0 树](usb-3-extensions.md#usb-3-tree)中 usb 设备上的终结点的相关信息。 此显示基于 USB 主机控制器扩展驱动程序所维护的数据结构，* (Ucx .sys) 。*

```dbgcmd
!usb3kd.ucx_endpoint UcxEndpointPrivContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UcxEndpointPrivContext______"></span><span id="_______ucxendpointprivcontext______"></span><span id="_______UCXENDPOINTPRIVCONTEXT______"></span>*UcxEndpointPrivContext*   
\_ \_ 表示终结点的 UCXENDPOINT PRIVCONTEXT 结构的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

USB 主机控制器扩展驱动程序 (Ucx*版本*.sys) 提供 usb 3.0 集线器驱动程序与 usb 3.0 主机控制器驱动程序之间的抽象层。 扩展驱动程序具有其自己的主机控制器、设备和终结点的表示形式。 输出 **！ ucx \_ endpoint** 命令基于扩展驱动程序所维护的数据结构。 有关 USB 主机控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序的详细信息，请参阅 [Usb 驱动程序堆栈体系结构](/windows-hardware/drivers/ddi/index)。

<a name="examples"></a>示例
--------

若要获取 UCX 终结点专用上下文的地址，请查看 [**！ UCX \_ controller \_ list**](-usb3kd-ucx-controller-list.md) 命令的输出。 在下面的示例中，第二个设备上的第一个终结点的专用上下文地址为0xfffffa8003694860。

```dbgcmd
3: kd> !ucx_controller_list

## Dumping List of UCX controller objects
--------------------------------------
[1] !ucx_controller 0xfffffa80052da050 (dt ucx01000!_UCXCONTROLLER_PRIVCONTEXT fffffa80052da050)
    !ucx_device 0xfffffa8005a41840
        .!ucx_endpoint 0xfffffa800533f3d0 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa80053405d0 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005a3f710 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005bbe4e0 [Blk Out], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa8005ac4810 [Blk In ], UcxEndpointStateStale
    !ucx_device 0xfffffa8005bd9680
        .!ucx_endpoint 0xfffffa8003694860 [Blk Out], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003686820 [Blk In ], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8005be0550 [Control], UcxEndpointStateEnabled
        .!ucx_endpoint 0xfffffa8003695580 [Blk In ], UcxEndpointStateStale
        .!ucx_endpoint 0xfffffa80036a20c0 [Blk Out], UcxEndpointStateStale
```

现在可以将 UCX 终结点专用上下文的地址传递给 **！ UCX \_ endpoint** 命令。

```dbgcmd
3: kd> !ucx_endpoint 0xfffffa8003694860

## Dumping Ucx USB Endpoint Information fffffa8003694860
-----------------------------------------------------
dt ucx01000!_UCXENDPOINT_PRIVCONTEXT 0xfffffa8003694860
[Blk Out], UcxEndpointStateEnabled, MaxTransferSize: 4194304
Endpoint Address: 0x02
Endpoint Queue: !wdfqueue 0x57ffc969888

UcxEndpoint State History: <Event> NewState 
    [ 3] <UcxEndpointEventOperationSuccess> UcxEndpointStateEnabled
    [ 2] <UcxEndpointEventYes> UcxEndpointStateCompletingPendingOperation1
    [ 1] <UcxEndpointEventEnableComplete> UcxEndpointStateIsAbleToStart2
    [ 0] <SmEngineEventStart> UcxEndpointStateCreated

UcxEndpoint Event History:
    [ 1] UcxEndpointEventEnableComplete
    [ 0] SmEngineEventStart

EventCallbacks:
    EvtEndpointPurge: (0xfffff880044ba6e8) USBXHCI!Endpoint_UcxEvtEndpointPurge
    EvtEndpointAbort: (0xfffff880044ba94c) USBXHCI!Endpoint_UcxEvtEndpointAbort
    EvtEndpointReset: (0xfffff880044bb854) USBXHCI!Endpoint_UcxEvtEndpointReset
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ usb3kd ucx \_ 控制器 \_ 列表**](-usb3kd-ucx-controller-list.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

