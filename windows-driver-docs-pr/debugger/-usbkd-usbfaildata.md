---
title: usbkd.usbfaildata
description: Usbkd.usbfaildata 命令显示有关 USB 设备存储的故障数据 （如果有）。
ms.assetid: 08FD3F82-73E3-4616-92EB-D562ECAB8A96
keywords:
- usbkd.usbfaildata Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbfaildata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55fdb43933f08d4ae24f466a86e3fbc99a74d167
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334114"
---
# <a name="usbkdusbfaildata"></a>!usbkd.usbfaildata


**！ Usbkd.usbfaildata**命令显示有关 USB 设备存储的故障数据 （如果有）。

```dbgcmd
!usbkd.usbfaildata PDO
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PDO______"></span><span id="_______pdo______"></span> *PDO*   
连接到 USB 集线器的设备的物理设备对象 (PDO) 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的是 PDO USB 设备的地址。 输入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

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

在上面的输出，显示作为建议命令的参数的地址 PDO **！ devstack ffffe00007c882a0**。

现在将传递给 PDO 的地址 **！ usbkd.usbfaildata**。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






