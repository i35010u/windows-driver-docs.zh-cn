---
title: usbkd.usbtt
description: Usbkd.usbtt 命令显示 USBPORT _TRANSACTION_TRANSLATOR 结构中的信息。
ms.assetid: 4D599BCE-C6C3-42B3-BDCE-EE9E47FA6AB7
keywords:
- usbkd.usbtt Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea628704feacbb584d83a36bd7355cf1587fe2cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327978"
---
# <a name="usbkdusbtt"></a>!usbkd.usbtt


**！ Usbkd.usbtt**命令显示中的信息**USBPORT ！\_事务\_转换器**结构。

```dbgcmd
!usbkd.usbtt StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
地址**usbport ！\_事务\_转换器**结构。 若要获得 USB 主控制器事务转换器列表，请使用[ **！ usbkd.usbhcdext** ](-usbkd-usbhcdext.md)命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的地址**usbport ！\_事务\_转换器**结构。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ ehci\_信息 ffffe00001ca11a0**。

单击 DML 命令或传递到设备扩展的地址[ **！ usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)若要获取的地址`GlobalTtListHead`。 传递到该地址[ **！ usbkd.usblist**](-usbkd-usblist.md)，随后会显示的地址**\_事务\_转换器**结构。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






