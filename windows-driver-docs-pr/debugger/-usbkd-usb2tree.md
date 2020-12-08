---
title: usbkd.usb2tree
description: Usbkd. usb2tree 命令显示 USB 2.0 树。
keywords:
- usbkd usb2tree Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usb2tree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1d06d5a53df7008aca2481ee4c0e3e899275a75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795183"
---
# <a name="usbkdusb2tree"></a>!usbkd.usb2tree


**！ Usbkd. usb2tree** 命令显示 [USB 2.0 树](usb-2-0-extensions.md#usb-2-tree)。

```dbgcmd
!usbkd.usb2tree
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


此屏幕截图显示了 **！ usb2tree** 命令的输出示例和示例。

![显示 uhci ehci 信息和枚举中心列表的！ usbkd. usb2tree 命令的输出](images/usb2tree01.png)

输出显示一个 EHCI 执行单元和两个 UHCI 执行单位。 本例中所示的执行单元恰好位于单个 USB 主机控制器设备上。 输出还显示根集线器和连接的设备。

输出使用 [ (DML) 的调试器标记语言 ](debugger-markup-language-commands.md) 来提供链接。 这些链接执行命令，以便为树中的对象指定相关的详细信息。 例如，你可以单击其中一个 [**！ devobj**](-devobj.md) 链接来获取与 EHCI 执行单元关联的功能设备对象的相关信息。 作为单击链接的替代方法，可以手动输入命令： **！ devobj ffffe00001ca7050**

**注意**  DML 功能在 WinDbg 中可用，但在 Visual Studio 或 KD 中不可用。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ Usb2tree** 命令是针对许多 [USB 2.0 调试程序扩展命令](usb-2-0-extensions.md)的父命令。 这些命令显示的信息基于这些驱动程序维护的数据结构：

-   usbehci.sys USB 2 主机控制器 (微型端口驱动程序) 
-   usbuhci.sys USB 2 主机控制器 (微型端口驱动程序) 
-   USB 2 主机控制器 (端口驱动程序的 usbport.sys) 
-    (USB 2 集线器驱动程序的 usbhub.sys) 

有关这些驱动程序的详细信息，请参阅 [Windows 中的 USB 主机端驱动程序](../usbcon/usb-3-0-driver-stack-architecture.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

