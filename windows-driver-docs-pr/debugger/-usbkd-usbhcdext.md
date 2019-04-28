---
title: usbkd.usbhcdext
description: Usbkd.usbhcdext 命令显示从 USB 主控制器或 USB 根集线器的设备扩展的信息。
ms.assetid: 83811F9F-5899-4EC8-83D7-39EE884C0A01
keywords:
- usbkd.usbhcdext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc5f93ee042ce918f3f5f7305a0176d4678ed69e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334096"
---
# <a name="usbkdusbhcdext"></a>!usbkd.usbhcdext


[ **！ Usbkd.usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)命令显示从 USB 主控制器或 USB 根集线器的设备扩展的信息。

```dbgcmd
!usbkd.usbhcdext DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
其中一个以下地址：

-   USB 主控制器的功能的设备对象 (FDO) 设备扩展。
-   物理设备对象 (PDO) USB 根集线器设备扩展。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的 EHCI 主机控制器 FDO 设备扩展的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
 ...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ ehci\_信息 ffffe00001ca11a0**。

现在将传递到设备扩展的地址[ **！ usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)命令。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
Operational Registers ffffd000228bf020
Device Data ffffe00001ca2da0
dt USBPORT!_FDO_EXTENSION ffffe00001ca15a0
DM Timer Flags ffffe00001ca16d4
FDO Flags ffffe00001ca16d0
HCD Log ffffe00001ca11a0

DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
EpNeoStateChangeList: !usblist ffffe00001ca2370, SC [Empty]
GlobalTtListHead: !usblist ffffe00001ca23a8, TT [Empty]
BusContextHead: !usblist ffffe00001ca16b0, BC 

## Pending Requests

[001] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe00001ca1450 Tag: AddD Obj: ffffe00001ca11a0
...

## XDPC List

01) dt USBPORT!_XDPC_CONTEXT ffffe00001ca1f18
...
```

下面是一种方法，若要查找的是 PDO 根中心的设备扩展的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
 ...
```

在上面的输出中可以看到的地址显示为该命令的参数的根集线器 FDO **！ devstack ffffe00002320050**。 使用[ **！ devstack** ](-devstack.md)命令来查找对 PDO 和 PDO 设备扩展的地址。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

在上面的输出，您可以看到的是 PDO 根中心的设备扩展的地址是`ffffe0000213c1a0`。

现在将传递到设备扩展的地址[ **！ usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)命令。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe0000213c1a0

Root Hub PDO Extension
Parent HC: FDO ffffe00001ca1050 !ehci_info ffffe00001ca11a0
HUB FDO ffffe00002320050 !hub2_info ffffe000023201a0
dt USBPORT!_PDO_EXTENSION ffffe0000213c5a0

## Pending Requests

[001] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe0000213c450 Tag: RHcr Obj: ffffe0000213c1a0
[002] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe00003ce5800 Tag: iIRP Obj: ffffe00002182210

## POWER FUNC HISTORY (latest at bottom)

[00] IRP_MN_WAIT_WAKE (PowerSystemHibernate)
...

## PnP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvPDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted 
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






