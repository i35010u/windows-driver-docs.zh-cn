---
title: usbkd.usbhuberr
description: Usbkd.usbhuberr 命令显示的 USB 集线器错误记录。
ms.assetid: 5BB87FA2-0531-400C-95B3-325EE4DDB649
keywords:
- usbkd.usbhuberr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhuberr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1593b60ec2a846d5ea8703211ba5faaf9881921
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334062"
---
# <a name="usbkdusbhuberr"></a>!usbkd.usbhuberr


**！ Usbkd.usbhuberr**命令显示的 USB 集线器错误记录。

```dbgcmd
!usbkd.usbhuberr StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
地址**usbhub ！\_集线器\_异常\_记录**结构。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的地址**usbhub ！\_集线器\_异常\_记录**。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
      ...
```

在上面的输出中可以看到建议的命令 **！ devstack ffffe00002320050**。 输入此命令。

```dbgcmd
0: kd> !kdexts.devstack ffffe000011f7050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe000011f7050  \Driver\usbhub     ffffe000011f71a0  0000006f
  ffffe00000a21050  \Driver\usbehci    ffffe00000a211a0  USBPDO-8
...
```

在上面的输出，`ffffe000011f71a0`是适用于中心的功能的设备对象 (FDO) 的设备扩展的地址。 传递到设备扩展的地址[ **！ usbkd.usbhubext**](-usbkd-usbhubext.md)。

```dbgcmd
0: kd> !usbkd.usbhubext ffffe000011f71a0

FDO ffffe000011f7050 PDO ffffe00000a21050 HubNumber# 7
dt USBHUB!_DEVICE_EXTENSION_HUB ffffe000011f71a0
!usbhublog ffffe000011f71a0
RemoveLock ffffe000011f7668
FdoFlags ffffe000011f7ba0

CurrentPowerIrp: System (0000000000000000) Device (0000000000000000)

ObjReferenceList: !usblist ffffe000011f7b70, RL 
ExceptionList: !usblist ffffe000011f8498, EL [Empty]
...
```

在上面的输出，`ffffe000011f8498`是例外列表的地址。 如果异常列表不为空，它将包含的地址**\_中心\_异常\_记录**结构。


## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






