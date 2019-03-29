---
title: usbkd.usb2tree
description: Usbkd.usb2tree 命令显示 USB 2.0 树。
ms.assetid: 6BEFE154-C8F0-466C-AB68-71C6304D0DEA
keywords:
- usbkd.usb2tree Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usb2tree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a47edbfe78880ed2ea784bf79c55e6ff9f1fb49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576656"
---
# <a name="usbkdusb2tree"></a>!usbkd.usb2tree


**！ Usbkd.usb2tree**命令将显示[USB 2.0 树](usb-2-0-extensions.md#usb-2-tree)。

```dbgcmd
!usbkd.usb2tree
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


此屏幕截图的输出示例 **！ usb2tree**命令。

![输出 ！ usbkd.usb2tree 命令显示 uhci ehci 信息和枚举的中心列表](images/usb2tree01.png)

该输出显示一个 EHCI 执行单元测试和两个 UHCI 执行单位。 此示例中所示的执行单元恰好位于单个 USB 主机控制器设备上。 输出还显示根集线器和连接的设备。

输出会使用[使用调试器标记语言 (DML)](debugger-markup-language-commands.md)提供链接。 链接执行命令来提供与树中的对象相关的详细的信息。 例如，可以单击其中一个[ **！ devobj** ](-devobj.md) EHCI 执行单元与关联的链接可获取有关功能的设备对象的信息。 作为单击的链接的替代方法，你可以输入该命令手动： **！ devobj ffffe00001ca7050**

**请注意**  DML 功能现已推出的 WinDbg 中，但未在 Visual Studio 或 KD。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ Usb2tree**命令是为许多父命令[USB 2.0 调试器扩展命令。](usb-2-0-extensions.md) 这些命令显示的信息基于由这些驱动程序维护的数据结构：

-   usbehci.sys （USB 2 主机控制器微型端口驱动程序）
-   usbuhci.sys （USB 2 主机控制器微型端口驱动程序）
-   usbport.sys （USB 2 主机控制器端口驱动程序）
-   usbhub.sys （USB 2 中心驱动程序）

有关这些驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p/?LinkId=251983)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






