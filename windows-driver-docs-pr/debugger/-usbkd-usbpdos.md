---
title: usbkd.usbpdos
description: Usbkd. usbpdos 命令显示有关 USB 集线器驱动程序创建 (PDOs) 的所有物理设备对象的信息。
ms.assetid: 2EFAC774-C400-4218-BF48-2D5DC557A83B
keywords:
- usbkd usbpdos Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbpdos
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ec07e7468fd592d98a9829df44d836e69262ac45
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217939"
---
# <a name="usbkdusbpdos"></a>!usbkd.usbpdos


**！ Usbkd usbpdos**命令显示有关 USB 集线器驱动程序创建 (PDOs) 的所有物理设备对象的信息。

```dbgcmd
!usbkd.usbpdos
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是 **！ usbpdos** 命令的输出示例。

```dbgcmd
0: kd> !usbkd.usbpdos

ext ffffe00006c513f0
VID 0a12 PID 0001 REV 0309 
 dt USBHUB!_USB_DEVICE_DESCRIPTOR ffffe00006c51960
Vendor: Xxxx
 Xxxx Corporation
 dd Class: (224)(e0)
 (224)(e0)
HubFdo: ffffe00000d94050, port: 2
<null>
SystemWake 5 SystemHibernate(S4)
wake_irp_list_head = ffffe00006c51cb0
wake_irp = ffffe00006c51cb0
PDO Times:
    Stat_PdoCreatedAt: 0d29bbd58
    Stat_PdoEnumeratedAt: b65ace75d29bbd58
    Stat: Enumeration Time: 0xa7d3842a(-1479310294) ms
    Stat_Pdo_SetD0_StartAt: 0d29bbd58
    Stat_Pdo_SetD0_CompleteAt: 0d29bbd58
    Stat: PDO Set_D0 time: 0x0(0) ms

## 

ext ffffe00007c883f0
VID 0781 PID 5530 REV 0100 
 dt USBHUB!_USB_DEVICE_DESCRIPTOR ffffe00007c88960
Vendor: Xxxx
 Xxxx Corporation
 dd Class: (0)(0)
 (8)Class_UsbStorage
HubFdo: ffffe00002320050, port: 3
:Xxxx  
SystemWake 5 SystemHibernate(S4)
wake_irp_list_head = ffffe00007c88cb0
wake_irp = ffffe00007c88cb0
PDO Times:
    Stat_PdoCreatedAt: 0d29bbd58
    Stat_PdoEnumeratedAt: 2380af52d29bbd58
    Stat: Enumeration Time: 0x9a24226c(-1708907924) ms
    Stat_Pdo_SetD0_StartAt: 0d29bbd58
    Stat_Pdo_SetD0_CompleteAt: 0d29bbd58
##     Stat: PDO Set_D0 time: 0x0(0) ms
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)