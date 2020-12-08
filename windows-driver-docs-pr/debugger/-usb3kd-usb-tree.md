---
title: usb3kd.usb_tree
description: Usb3kd.usb_tree 扩展以树格式显示有关计算机上所有 USB 3.0 控制器、集线器和设备的信息。
keywords:
- usb3kd.usb_tree Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.usb_tree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 05ca66897c915836b753761fd2ba31498e88e9eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814035"
---
# <a name="usb3kdusb_tree"></a>！ usb3kd \_ 树


[**！ Usb3kd \_ 树**](-usb3kd-device-info.md)扩展以树格式显示有关计算机上的所有 usb 3.0 控制器、集线器和设备的信息。

```dbgcmd
!usb3kd.usb_tree [1]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______1______"></span>**1**   
显示内容包括集线器和端口的状态信息。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


以下屏幕截图显示了 [**！ usb \_ 树**](-usb3kd-device-info.md) 命令的输出。

![\-显示拓扑枚举设备和集线器列表的！ usb 树命令的输出](images/usbtree01.png)

输出显示有一个 USB 3.0 主机控制器，它由以 [**！ xhci \_ info**](-usb3kd-xhci-info.md)开头的行表示。 下一行表示主机控制器的根集线器。 接下来的四行表示与根集线器关联的端口。 你可以看到两个端口已连接设备。

输出使用 [ (DML) 的调试器标记语言 ](debugger-markup-language-commands.md) 来提供链接。 这些链接执行命令，以便为树中的各个对象指定详细信息。 例如，你可以通过单击其中一个 " [**设备 \_ 信息**](-usb3kd-device-info.md) " 链接来获取有关某个连接的设备的信息。 作为单击链接的替代方法，可以输入命令。 例如，若要查看有关第一个连接的设备的信息，可以输入命令 **！设备 \_ 信息 0xfffffa8004630690**。

**注意**  DML 功能在 WinDbg 中可用，但在 Visual Studio 或 KD 中不可用。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

[**！ Usb \_ tree**](-usb3kd-device-info.md)命令是此命令集的父命令。

-   [**！中心 \_ 信息**](-usb3kd-hub-info.md)
-   [**！中心 \_ 信息 \_ 来自 \_ fdo**](-usb3kd-hub-info-from-fdo.md)
-   [**！设备 \_ 信息**](-usb3kd-device-info.md)
-   [**！ \_ \_ 来自 pdo 的设备信息 \_**](-usb3kd-device-info-from-pdo.md)
-   [**！端口 \_ 信息**](-usb3kd-port-info.md)

[**！ Usb \_ 树**](-usb3kd-device-info.md)系列命令显示的信息取决于 usb 3.0 集线器驱动程序所维护的数据结构。 有关 usb 3.0 集线器驱动程序和 USB 3.0 堆栈中其他驱动程序的信息，请参阅 [Usb 驱动程序堆栈体系结构](../usbcon/usb-3-0-driver-stack-architecture.md)。 有关 USB 3.0 堆栈中的驱动程序所使用的数据结构的说明，请参阅 [Windows 8 视频中 USB 调试革新](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P) 的第2部分。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

