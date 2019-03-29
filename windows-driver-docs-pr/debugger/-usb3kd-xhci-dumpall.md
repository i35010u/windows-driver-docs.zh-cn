---
title: usb3kd.xhci_dumpall
description: Usb3kd.xhci_dumpall 命令显示计算机上的所有 USB 3.0 主机控制器的信息。 显示基于由 UsbXhci.sys 维护的数据结构。
ms.assetid: D1087DC6-B065-48E3-93B2-EF53AE9DA8C7
keywords:
- usb3kd.xhci_dumpall Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_dumpall
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7736dba8fbb19b3b0e73e7fe5a2cea85cfa7fae6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564296"
---
# <a name="usb3kdxhcidumpall"></a>!usb3kd.xhci\_dumpall


[ **！ Usb3kd.xhci\_dumpall** ](-usb3kd-device-info.md)命令的计算机上显示有关所有 USB 3.0 主机控制器的信息。 显示基于 USB 3.0 主机控制器驱动程序 (UsbXhci.sys) 维护的数据结构。

```dbgcmd
!usb3kd.xhci_dumpall [1]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_____________1"></span> **1**  
运行所有 XHCI 命令并显示每个命令的输出。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


下面的屏幕截图显示的输出 **！ xhci\_dumpall**l 命令。

![输出 ！ xhci\-dumpall 命令显示 xhci 控制器的信息](images/xhcidumpall01.png)

输出显示一个 USB 3.0 主控制器。

输出会使用[使用调试器标记语言 (DML)](debugger-markup-language-commands.md)提供链接。 链接执行提供主机控制器的状态，有关详细的信息，因为它保持了 USB 3.0 主机控制器驱动程序的命令。 例如，你可以获取有关主机的详细的信息控制器功能通过单击[ **！ xhci\_功能**](-usb3kd-xhci-capability.md)链接。 作为单击的链接的替代方法，你可以输入命令。 例如，若要查看主控制器的资源使用情况信息，可以输入命令 **！ xhci\_resourceusage 0xfffffa800536e2d0**。

**请注意**  DML 功能现已推出的 WinDbg 中，但未在 Visual Studio 或 KD。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ Xhci\_dumpall**命令是此命令集的父命令。

-   [**!xhci\_capability**](-usb3kd-xhci-capability.md)
-   [**!xhci\_info**](-usb3kd-xhci-info.md)
-   [**!xhci\_deviceslots**](-usb3kd-xhci-deviceslots.md)
-   [**!xhci\_commandring**](-usb3kd-xhci-commandring.md)
-   [**!xhci\_eventring**](-usb3kd-xhci-eventring.md)
-   [**!xhci\_transferring**](-usb3kd-xhci-transferring.md)
-   [**!xhci\_trb**](-usb3kd-xhci-trb.md)
-   [**!xhci\_registers**](-usb3kd-xhci-registers.md)
-   [**!xhci\_resourceusage**](-usb3kd-xhci-resourceusage.md)

显示的信息 **！ xhci\_dumpall** USB 3.0 主机控制器驱动程序维护的数据结构为基础的命令系列。 USB 3.0 主机控制器驱动程序和 USB 3.0 堆栈中的其他驱动程序有关的信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。 使用 USB 3.0 堆栈中的驱动程序的数据结构的说明，请参阅的第 2 部分[USB 调试 Windows 8 中创新](https://go.microsoft.com/fwlink/p/?LinkID=249153)视频。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






