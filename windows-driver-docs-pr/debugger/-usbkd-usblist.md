---
title: usbkd.usblist
description: Usbkd.usblist 命令显示链接的列表的指定类型的结构。
ms.assetid: 503466EE-2246-4CE3-BCE7-6DC7D42DB86A
keywords:
- usbkd.usblist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usblist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b20b0269a625cd019d42859a06b037946197625b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367989"
---
# <a name="usbkdusblist"></a>!usbkd.usblist


**！ Usbkd.usblist**命令显示链接的列表的指定类型的结构。

```dbgcmd
!usbkd.usblist ListAddr, ListType
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______ListAddr______"></span><span id="_______listaddr______"></span><span id="_______LISTADDR______"></span> *ListAddr*   
结构的链接列表的地址。 若要查找所维护的 USB 端口驱动程序的链接列表的地址，请使用[ **！ usbhcdext**](-usbkd-usbhcdext.md)。 若要查找的维护的 USB 集线器驱动程序的链接列表的地址，请使用[ **！ usbhubext**](-usbkd-usbhubext.md)。

<span id="_______ListType______"></span><span id="_______listtype______"></span><span id="_______LISTTYPE______"></span> *ListType*   
以下列表类型之一。

| 列表类型 | 结构                                |
|-----------|------------------------------------------|
| **BC**    | **usbport ！\_总线\_上下文**               |
| **EP**    | **usbport!\_HCD\_ENDPOINT**              |
| **TT**    | **usbport ！\_事务\_转换器**    |
| **DL**    | **usbport!\_USBD\_DEVICE\_HANDLE**       |
| **PL**    | **usbhub!\_DEVICE\_EXTENSION\_PDO**      |
| **EL**    | **usbhub ！\_集线器\_异常\_记录**      |
| **RL**    | **usbhub ！\_集线器\_引用\_列表\_条目** |
| **TL**    | **usbhub ！\_集线器\_计时器\_对象**          |
| **WI**    | **usbhub ！\_中心\_工作项**               |
| **IO**    | **usbhub ！\_IO\_列表\_条目**             |
| **LA**    | **usbhub ！\_闩锁\_列表\_条目**          |
| **CL**    | **usbhub ！\_端口\_更改\_上下文**       |
| **BL**    | **usbhub ！\_SSP\_忙\_处理**           |

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法来查找链接列表的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 ...
   ...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ ehci\_信息 ffffe00001ca11a0**。

单击 DML 命令或传递到设备扩展的地址[ **！ usbhcdext**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-usbkd-usbhcdext)。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL
...
```

链接列表的地址是在上面的输出，ffffe00001ca23b8 **usbport ！\_USBD\_设备\_处理**结构。

现在将传递到链接列表的地址 **！ usblist**。

```dbgcmd
0: kd> !usblist ffffe00001ca23b8, DL
list: ffffe00001ca23b8 DL
----------
!usbdevh ffffe000020f9590
SSP [IdleReady] (0)
PCI\VEN_Xxxx  Xxxx Corporation
Root Hub
DriverName :  
----------
!usbdevh ffffe00001bce250
SSP [IdleReady] (0)
USB\Xxxx  Xxxx Corporation
Speed: HIGH, Address:  1, PortPathDepth: 1, PortPath: [3 0 0 0 0 0]
DriverName :\Driver\USBSTOR      !devstack ffffe000053ef2a0
----------
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






