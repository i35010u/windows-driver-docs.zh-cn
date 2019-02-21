---
title: usbkd.usbchain
description: Usbkd.usbchain 命令显示指定 PDO，从开始，要返回到根集线器的 USB 设备链。
ms.assetid: 0D69E29E-3886-436F-B5EE-E4F297D9CE36
keywords:
- usbkd.usbchain Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbchain
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73c13d57af32bc852b650a829e9a5148b02adc2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548230"
---
# <a name="usbkdusbchain"></a>!usbkd.usbchain


**！ Usbkd.usbchain**命令显示指定 PDO，从开始，要返回到根集线器的 USB 设备链。

```dbgcmd
!usbkd.usbchain PDO
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PDO______"></span><span id="_______pdo______"></span> *PDO*   
连接到 USB 集线器的设备的物理设备对象 (PDO) 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的是 PDO USB 设备的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
 kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
        Port 1: !port2_info ffffe000021bf000 
        Port 2: !port2_info ffffe000021bfb40 
        Port 3: !port2_info ffffe000021c0680 !devstack ffffe00007c882a0
...
```

在上面的输出中的 PDO 地址是建议的命令的参数 **！ devstack ffffe00007c882a0**。 传递给 PDO 的地址 **！ usbkd.usbchain**。

```dbgcmd
0: kd> !usbkd.usbchain ffffe00007c882a0

usbchain
*****************************************************************************
HUB PDO ffffe00007c882a0 on port 3 !usbhubext ffffe00007c883f0 ArmedForWake = 0
VID Xxxx PID Xxxx REV 0100  Xxxx Corporation
    HUB #3 FDO ffffe00002320050 , !usbhubext ffffe000023201a0  HWC_ARM=0
    ROOT HUB PDO(ext) @ffffe0000213c1a0
        ROOT HUB FDO @ffffe00001ca1050, !usbhcdext ffffe00001ca11a0 PCI Vendor:Device:...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






