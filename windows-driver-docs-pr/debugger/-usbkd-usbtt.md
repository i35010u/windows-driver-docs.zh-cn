---
title: usbkd.usbtt
description: Usbkd. usbtt 命令显示 USBPORT _TRANSACTION_TRANSLATOR 结构中的信息。
ms.assetid: 4D599BCE-C6C3-42B3-BDCE-EE9E47FA6AB7
keywords:
- usbkd usbtt Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e8baa90ae6cb985cd6c1f93f3e2c7826e9d7c3a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217923"
---
# <a name="usbkdusbtt"></a>!usbkd.usbtt


**！ Usbkd. usbtt**命令显示 USBPORT 中的信息 **！ \_事务 \_ 转换器**结构。

```dbgcmd
!usbkd.usbtt StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbport 的地址 **！ \_事务 \_ 转换器** 结构。 若要获取 USB 主机控制器的事务转换器列表，请使用 [**！ usbkd. usbhcdext**](-usbkd-usbhcdext.md) 命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找 usbport 地址的一种方法 **！ \_事务 \_ 转换器** 结构。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

在上面的输出中，FDO 的设备扩展的地址显示为 [DML](debugger-markup-language-commands.md) 命令 **！ ehci \_ info ffffe00001ca11a0**的参数。

单击 DML 命令或将设备扩展的地址传递给 [**！ usbhcdext**](-usbkd-usbhcdext.md) ，以获取的地址 `GlobalTtListHead` 。 将该地址传递给[**！ usbkd. usblist**](-usbkd-usblist.md)，这将显示** \_ 事务 \_ 转换器**结构的地址。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

