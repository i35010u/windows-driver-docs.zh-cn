---
title: usbkd.usbhcdpnp
description: Usbkd. usbhcdpnp 命令显示 USB 主机控制器或根集线器的即插即用 (PnP) 状态历史记录。
keywords:
- usbkd usbhcdpnp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdpnp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6a049a84a23c354aaca8ba9b376983c4630e9ff8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818677"
---
# <a name="usbkdusbhcdpnp"></a>!usbkd.usbhcdpnp


**！ Usbkd. usbhcdpnp** 命令显示 USB 主机控制器或根集线器的即插即用 (PnP) 状态历史记录。

```dbgcmd
!usbkd.usbhcdpnp DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
以下项之一的地址：

-   功能设备对象的设备扩展 (USB 主机控制器的 FDO) 。
-    (PDO) USB 根集线器的物理设备对象的设备扩展。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种查找 USB 主机控制器 FDO 的设备扩展地址的方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree

UHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe0000090c3d0
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

在上面的输出中，FDO 的设备扩展的地址显示为 [DML](debugger-markup-language-commands.md) command **！ uhci \_ info ffffe00001c8f1a0** 的参数。

现在，将设备扩展的地址传递给 **！ usbhcdpnp** 命令。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00001c8f1a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvFDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
[02] EvFDO_IRP_MN_QBR_RH            PnpStarted          PnpStarted
```

下面是一种查找根集线器 PDO 的设备扩展地址的方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
    RootHub !hub2_info ffffe00000d941a0 !devstack ffffe00000d94050
```

在上面的输出中，可以看到根集线器的 FDO 地址，该地址显示为命令 **！ devstack ffffe00000d94050** 的参数。 使用 [**！ devstack**](-devstack.md) 命令查找 pdo 的地址和 pdo 设备扩展。

```dbgcmd
0: kd> !kdexts.devstack ffffe00000d94050
  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00000d94050  \Driver\usbhub     ffffe00000d941a0  0000006b
  ffffe00000ed4050  \Driver\usbuhci    ffffe00000ed41a0  USBPDO-2
```

在上面的输出中，可以看到根集线器的 PDO 的设备扩展地址是 `ffffe00000ed41a0` 。

现在，将设备扩展的地址传递给 **！ usbhcdpnp** 命令。

```dbgcmd
0: kd> !usbkd.usbhcdpnp ffffe00000ed41a0

## PNP STATE LOG (latest at bottom)

##      EVENT                         STATE               NEXT

[01] EvPDO_IRP_MN_START_DEVICE      PnpNotStarted       PnpStarted          
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

