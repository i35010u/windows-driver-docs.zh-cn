---
title: usbkd.usbhcdpnp
description: Usbkd.usbhcdpnp 命令显示有关 USB 主控制器或根集线器插即用 (PnP) 状态历史记录。
ms.assetid: 1153F3C2-5878-4223-AA18-5AE6FA056851
keywords:
- usbkd.usbhcdpnp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpnp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3a2ad2c4287a694f2ee39b5b1fd1b2df809a65e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519635"
---
# <a name="usbkdusbhcdpnp"></a>!usbkd.usbhcdpnp


**！ Usbkd.usbhcdpnp**命令显示有关 USB 主控制器或根集线器插即用 (PnP) 状态历史记录。

```dbgcmd
!usbkd.usbhcdpnp DeviceExtension
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

下面是查找 FDO 的 USB 主控制器的地址的设备扩展的一种方法。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree

UHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe0000090c3d0
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ uhci\_信息 ffffe00001c8f1a0**。

现在将传递到设备扩展的地址 **！ usbhcdpnp**命令。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00001c8f1a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvFDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
[02] EvFDO_IRP_MN_QBR_RH            PnpStarted          PnpStarted
```

下面是一种方法，若要查找的是 PDO 根中心的设备扩展的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
    RootHub !hub2_info ffffe00000d941a0 !devstack ffffe00000d94050
```

在上面的输出中可以看到的地址显示为该命令的参数的根集线器 FDO **！ devstack ffffe00000d94050**。 使用[ **！ devstack** ](-devstack.md)命令来查找对 PDO 和 PDO 设备扩展的地址。

```dbgcmd
0: kd> !kdexts.devstack ffffe00000d94050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00000d94050  \Driver\usbhub     ffffe00000d941a0  0000006b
  ffffe00000ed4050  \Driver\usbuhci    ffffe00000ed41a0  USBPDO-2
```

在上面的输出，您可以看到的是 PDO 根中心的设备扩展的地址是`ffffe00000ed41a0`。

现在将传递到设备扩展的地址 **！ usbhcdpnp**命令。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00000ed41a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvPDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






