---
title: usbkd.usbchain
description: Usbkd. usbchain 命令显示从指定 PDO 开始，并返回到根集线器的 USB 设备链。
keywords:
- usbkd usbchain Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbchain
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9d180d15c442c2de8f6cd9f0118036abb8db856c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814025"
---
# <a name="usbkdusbchain"></a>!usbkd.usbchain


**！ Usbkd. usbchain** 命令显示从指定 PDO 开始，并返回到根集线器的 USB 设备链。

```dbgcmd
!usbkd.usbchain PDO
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PDO______"></span><span id="_______pdo______"></span>*PDO*   
连接到 USB 集线器的设备 (PDO) 的物理设备对象的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找 USB 设备的 PDO 地址的一种方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

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

在上面的输出中，PDO 的地址是建议的命令的参数 **！ devstack ffffe00007c882a0**。 将 PDO 的地址传递给 **！ usbkd. usbchain**。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

