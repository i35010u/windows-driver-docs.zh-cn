---
title: usb3kd port_info
description: Port_info usb3kd 命令显示有关 USB 3.0 树中 USB 端口的信息。
ms.assetid: 78233FE5-981E-42C4-A100-198CAAA840A0
keywords:
- usb3kd port_info Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.port_info
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab4a100ef4dd443f609f939b976d38a3c52f3c20
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206837"
---
# <a name="usb3kdport_info"></a>！ usb3kd \_ 信息


[**！ Usb3kd \_ info**](-usb3kd-device-info.md)命令显示有关[USB 3.0 树](usb-3-extensions.md#usb-3-tree)中 usb 端口的信息。

```dbgcmd
!usb3kd.port_info PortContext
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PortContext______"></span><span id="_______portcontext______"></span><span id="_______PORTCONTEXT______"></span>*PortContext*   
\_端口 \_ 上下文结构的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="examples"></a>示例
--------

若要获取端口上下文的地址，请查看 [**！ usb \_ 树**](-usb3kd-usb-tree.md) 命令的输出。 在下面的示例中，端口上下文的地址为0xfffffa8005abe0c0。

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

现在，可以将端口上下文的地址传递给 **！端口 \_ 信息** 命令。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

