---
title: usbkd.usblist
description: Usbkd. usblist 命令显示指定类型的结构的链接列表。
keywords:
- usbkd usblist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usblist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b422a8e1ddbdf044c3ed0390fb6bdf511a9011f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788921"
---
# <a name="usbkdusblist"></a>!usbkd.usblist


**！ Usbkd. usblist** 命令显示指定类型的结构的链接列表。

```dbgcmd
!usbkd.usblist ListAddr, ListType
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______ListAddr______"></span><span id="_______listaddr______"></span><span id="_______LISTADDR______"></span>*ListAddr*   
结构的链接列表的地址。 若要查找 USB 端口驱动程序所维护的链接列表的地址，请使用 [**！ usbhcdext**](-usbkd-usbhcdext.md)。 若要查找由 USB 集线器驱动程序维护的链接列表的地址，请使用 [**！ usbhubext**](-usbkd-usbhubext.md)。

<span id="_______ListType______"></span><span id="_______listtype______"></span><span id="_______LISTTYPE______"></span>*ListType*   
以下列表类型之一。

| 列表类型 | 结构                                |
|-----------|------------------------------------------|
| **BC**    | **usbport！ \_总线 \_ 上下文**               |
| **EP**    | **usbport！ \_HCD \_ 终结点**              |
| **TT**    | **usbport！ \_事务 \_ 转换器**    |
| **磁盘**    | **usbport！ \_USBD \_ 设备 \_ 句柄**       |
| **PL**    | **usbhub！ \_设备 \_ 扩展 \_ PDO**      |
| **EL**    | **usbhub！ \_中心 \_ 异常 \_ 记录**      |
| **RL**    | **usbhub！ \_中心 \_ 引用 \_ 列表 \_ 条目** |
| **TL**    | **usbhub！ \_中心 \_ 计时器 \_ 对象**          |
| **WI**    | **usbhub！ \_中心 \_ 工作项**               |
| **排**    | **usbhub！ \_IO \_ 列表 \_ 条目**             |
| **LA**    | **usbhub！ \_闩锁 \_ 列表 \_ 项**          |
| **CL**    | **usbhub！ \_端口 \_ 更改 \_ 上下文**       |
| **BL**    | **usbhub！ \_SSP \_ 繁忙 \_ 句柄**           |

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找链接列表地址的一种方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 ...
   ...
```

在上面的输出中，FDO 的设备扩展的地址显示为 [DML](debugger-markup-language-commands.md) 命令 **！ ehci \_ info ffffe00001ca11a0** 的参数。

单击 DML 命令或将设备扩展的地址传递给 [**！ usbhcdext**](-usbkd-usbhcdext.md)。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL
...
```

在上面的输出中，ffffe00001ca23b8 是 usbport 的链接列表的地址 **！ \_USBD \_ 设备 \_ 句柄** 结构。

现在，将链接列表的地址传递给 **！ usblist**。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

