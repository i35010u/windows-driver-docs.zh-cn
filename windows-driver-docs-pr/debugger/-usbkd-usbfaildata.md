---
title: usbkd.usbfaildata
description: 如果为 USB 设备存储了任何) ，usbkd. usbfaildata 命令将显示失败数据 (。
ms.assetid: 08FD3F82-73E3-4616-92EB-D562ECAB8A96
keywords:
- usbkd usbfaildata Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbfaildata
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9661abb872986739ecf72dbcff08b274eb03b6db
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213513"
---
# <a name="usbkdusbfaildata"></a>!usbkd.usbfaildata


如果为 USB 设备存储了任何) ，则 **！ usbkd. usbfaildata** 命令将显示失败数据 (。

```dbgcmd
!usbkd.usbfaildata PDO
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PDO______"></span><span id="_______pdo______"></span>*PDO*   
连接到 USB 集线器的设备 (PDO) 的物理设备对象的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找 USB 设备的 PDO 地址的一种方法。 输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

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

在上面的输出中，PDO 的地址显示为建议命令的参数 **！ devstack ffffe00007c882a0**。

现在，将 PDO 的地址传递给 **！ usbkd. usbfaildata**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

