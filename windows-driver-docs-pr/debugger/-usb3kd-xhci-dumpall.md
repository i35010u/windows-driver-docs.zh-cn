---
title: usb3kd xhci_dumpall
description: Xhci_dumpall usb3kd 命令显示有关计算机上的所有 USB 3.0 主机控制器的信息。 该显示基于 UsbXhci.sys 维护的数据结构。
ms.assetid: D1087DC6-B065-48E3-93B2-EF53AE9DA8C7
keywords:
- usb3kd xhci_dumpall Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_dumpall
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4661b2255fa14d06c452cf58b6ea66fdbfa7a4b2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216304"
---
# <a name="usb3kdxhci_dumpall"></a>！ usb3kd. xhci \_ dumpall


[**！ Usb3kd. xhci \_ dumpall**](-usb3kd-device-info.md)命令显示有关计算机上的所有 USB 3.0 主机控制器的信息。 显示基于 USB 3.0 主机控制器驱动程序所维护的数据结构 ( # A0) 。

```dbgcmd
!usb3kd.xhci_dumpall [1]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_____________1"></span> **1**  
运行所有 XHCI 命令，并显示每个命令的输出。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


以下屏幕截图显示 **！ xhci \_ dumpall**l 命令的输出。

![\-显示 xhci 控制器信息的！ xhci dumpall 命令的输出](images/xhcidumpall01.png)

输出显示有一个 USB 3.0 主机控制器。

输出使用 [ (DML) 的调试器标记语言 ](debugger-markup-language-commands.md) 来提供链接。 这些链接执行命令，这些命令可为 USB 3.0 主机控制器驱动程序维护的主机控制器的状态获得详细信息。 例如，可以通过单击 [**！ xhci \_ 功能**](-usb3kd-xhci-capability.md) 链接获取有关主机控制器功能的详细信息。 作为单击链接的替代方法，可以输入命令。 例如，若要查看有关主机控制器资源使用情况的信息，可以输入 command **！ xhci \_ resourceusage 0xfffffa800536e2d0**。

**注意**   DML 功能在 WinDbg 中可用，但在 Visual Studio 或 KD 中不可用。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ Xhci \_ dumpall**命令是此命令集的父命令。

-   [**！ xhci \_ 功能**](-usb3kd-xhci-capability.md)
-   [**！ xhci \_ 信息**](-usb3kd-xhci-info.md)
-   [**！ xhci \_ deviceslots**](-usb3kd-xhci-deviceslots.md)
-   [**！ xhci \_ commandring**](-usb3kd-xhci-commandring.md)
-   [**！ xhci \_ eventring**](-usb3kd-xhci-eventring.md)
-   [**！ xhci \_ 传输**](-usb3kd-xhci-transferring.md)
-   [**！ xhci \_ trb**](-usb3kd-xhci-trb.md)
-   [**！ xhci \_ 注册**](-usb3kd-xhci-registers.md)
-   [**！ xhci \_ resourceusage**](-usb3kd-xhci-resourceusage.md)

**！ Xhci \_ dumpall**系列命令显示的信息基于 USB 3.0 主机控制器驱动程序所维护的数据结构。 有关 usb 3.0 主机控制器驱动程序和 USB 3.0 堆栈中其他驱动程序的信息，请参阅 [Usb 驱动程序堆栈体系结构](../usbcon/usb-3-0-driver-stack-architecture.md)。 有关 USB 3.0 堆栈中的驱动程序所使用的数据结构的说明，请参阅 [Windows 8 视频中 USB 调试革新](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P) 的第2部分。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

