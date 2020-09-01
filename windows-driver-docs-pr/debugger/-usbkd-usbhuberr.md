---
title: usbkd.usbhuberr
description: Usbkd. usbhuberr 命令显示 USB 集线器错误记录。
ms.assetid: 5BB87FA2-0531-400C-95B3-325EE4DDB649
keywords:
- usbkd usbhuberr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhuberr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6f4dfd68341471f7c9fa1abc6371f55665a43b93
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207371"
---
# <a name="usbkdusbhuberr"></a>!usbkd.usbhuberr


**！ Usbkd. usbhuberr**命令显示 USB 集线器错误记录。

```dbgcmd
!usbkd.usbhuberr StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbhub 的地址 **！ \_中心 \_ 异常 \_ 记录** 结构。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找 usbhub 地址的一种方法 **！ \_中心 \_ 异常 \_ 记录**。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
      ...
```

在上面的输出中，可以看到建议的命令 **！ devstack ffffe00002320050**。 输入此命令：

```dbgcmd
0: kd> !kdexts.devstack ffffe000011f7050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe000011f7050  \Driver\usbhub     ffffe000011f71a0  0000006f
  ffffe00000a21050  \Driver\usbehci    ffffe00000a211a0  USBPDO-8
...
```

在上面的输出中， `ffffe000011f71a0` 是中心 (FDO) 的功能设备对象的设备扩展的地址。 将设备扩展的地址传递给 [**！ usbkd. usbhubext**](-usbkd-usbhubext.md)。

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

在上面的输出中， `ffffe000011f8498` 是异常列表的地址。 如果异常列表不为空，它将包含** \_ 中心 \_ 异常 \_ 记录**结构的地址。


## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

