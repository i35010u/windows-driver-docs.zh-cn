---
title: usb3kd.port_info
description: Usb3kd.port_info 命令在 USB 3.0 树中显示有关 USB 端口的信息。
ms.assetid: 78233FE5-981E-42C4-A100-198CAAA840A0
keywords:
- usb3kd.port_info Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.port_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 015237962c3954dc7bf8fa1bff283425fe838398
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338720"
---
# <a name="usb3kdportinfo"></a>!usb3kd.port\_info


[ **！ Usb3kd.port\_信息**](-usb3kd-device-info.md)命令显示有关中的 USB 端口信息[USB 3.0 树](usb-3-extensions.md#usb-3-tree)。

```dbgcmd
!usb3kd.port_info PortContext
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PortContext______"></span><span id="_______portcontext______"></span><span id="_______PORTCONTEXT______"></span> *PortContext*   
地址\_端口\_上下文结构。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="examples"></a>示例
--------

若要获取端口上下文的地址，请查看的输出[ **！ usb\_树**](-usb3kd-usb-tree.md)命令。 在以下示例中，端口上下文的地址是 0xfffffa8005abe0c0。

```dbgcmd
3: kd> !usb_tree

## Dumping HUB Tree - !drvObj 0xfffffa800597f770
--------------------------------------------

Topology
--------
1)  !xhci_info 0xfffffa80051d1940  ... - PCI: VendorId ...
    !hub_info 0xfffffa8005ad92d0 (ROOT)
        ...
        !port_info 0xfffffa8005abe0c0 !device_info 0xfffffa8005abd0c0 Desc: ... USB Flash Drive Speed: Super
```

现在可以将传递到端口上下文的地址 **！ 端口\_信息**命令。

```dbgcmd
3: kd> !port_info 0xfffffa8005abe0c0

## Dumping Port Context 0xfffffa8005abe0c0
---------------------------------------
dt USBHUB3!_PORT_CONTEXT 0xfffffa8005abe0c0
!hub_info 0xfffffa8005ad92d0 (dt _HUB_FDO_CONTEXT 0xfffffa8005ad92d0)
!device_info 0xfffffa8005abd0c0 (dt _DEVICE_CONTEXT 0xfffffa8005abd0c0)
!rcdrlogdump usbhub3 -a 0xfffffa8005abf6b0

PortNumber: 2
Last Port Status(3.0): Connected Enabled Powered
Last Port Change: <none>

CurrentPortEvent: PsmEventPortConnectChange
Current Port(3.0) State: ConnectedEnabled.WaitingForPortChangeEvent

Port(3.0) State History: <Event> NewState (<Operation>(),..) :

    [34] <Push> WaitingForPortChangeEvent 
    ...
Port Event History:
    [ 8] TransferSuccess
    ...  
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






