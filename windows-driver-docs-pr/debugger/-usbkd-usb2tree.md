---
title: usbkd.usb2tree
description: Usbkd. usb2tree 命令显示 USB 2.0 树。
ms.assetid: 6BEFE154-C8F0-466C-AB68-71C6304D0DEA
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
ms.openlocfilehash: c965428d3db1d3db617515903fba3bf90a8553b1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534868"
---
# <a name="usbkdusb2tree"></a>!usbkd.usb2tree


**！ Usbkd. usb2tree**命令显示[USB 2.0 树](usb-2-0-extensions.md#usb-2-tree)。

```dbgcmd
!usbkd.usb2tree
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


此屏幕截图显示了 **！ usb2tree**命令的输出示例和示例。

![显示 uhci ehci 信息和枚举中心列表的！ usbkd. usb2tree 命令的输出](images/usb2tree01.png)

输出显示一个 EHCI 执行单元和两个 UHCI 执行单位。 本例中所示的执行单元恰好位于单个 USB 主机控制器设备上。 输出还显示根集线器和连接的设备。

输出使用[调试器标记语言（DML）](debugger-markup-language-commands.md)来提供链接。 这些链接执行命令，以便为树中的对象指定相关的详细信息。 例如，你可以单击其中一个[**！ devobj**](-devobj.md)链接来获取与 EHCI 执行单元关联的功能设备对象的相关信息。 作为单击链接的替代方法，可以手动输入命令： **！ devobj ffffe00001ca7050**

**注意**   DML 功能在 WinDbg 中可用，但在 Visual Studio 或 KD 中不可用。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd

<a name="remarks"></a>注解
-------

**！ Usb2tree**命令是针对许多[USB 2.0 调试程序扩展命令](usb-2-0-extensions.md)的父命令。 这些命令显示的信息基于这些驱动程序维护的数据结构：

-   usbehci （用于 USB 2 主机控制器的微型端口驱动程序）
-   usbuhci （用于 USB 2 主机控制器的微型端口驱动程序）
-   usbport （USB 2 主机控制器的端口驱动程序）
-   usbhub （USB 2 集线器驱动程序）

有关这些驱动程序的详细信息，请参阅[Windows 中的 USB 主机端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






