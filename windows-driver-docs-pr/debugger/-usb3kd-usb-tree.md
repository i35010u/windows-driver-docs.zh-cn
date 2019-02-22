---
title: usb3kd.usb_tree
description: Usb3kd.usb_tree 扩展的信息，以树格式显示，有关所有 USB 3.0 控制器、 中心和设备的计算机上。
ms.assetid: 8E24AD44-7B32-4299-8428-D8E9B36F5848
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
ms.openlocfilehash: d6a8fef0d862caa8025ffb7b104746217264364b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544351"
---
# <a name="usb3kdusbtree"></a>!usb3kd.usb\_tree


[ **！ Usb3kd.usb\_树**](-usb3kd-device-info.md)扩展的信息，以树格式显示，有关所有 USB 3.0 控制器、 中心和设备的计算机上。

```dbgcmd
!usb3kd.usb_tree [1]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______1______"></span> **1**   
显示内容包括中心和端口的状态信息。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


以下屏幕截图显示的输出[ **！ usb\_树**](-usb3kd-device-info.md)命令。

![输出 ！ usb\-树结构命令显示拓扑枚举的设备和中心列表](images/usbtree01.png)

输出显示有一个 USB 3.0 主控制器，由开头的行[ **！ xhci\_信息**](-usb3kd-xhci-info.md)。 下一步的行表示主控制器的根中心。 接下来的四线表示与根中心关联的端口。 您可以看到两个端口已连接的设备。

输出会使用[使用调试器标记语言 (DML)](debugger-markup-language-commands.md)提供链接。 链接执行命令，在树中的单个对象的详细的信息。 例如，可以通过单击之一来获取有关某个已连接设备的信息[ **！ 设备\_信息**](-usb3kd-device-info.md)链接。 作为单击的链接的替代方法，你可以输入命令。 例如，若要查看有关第一个连接的设备的信息，可以输入命令 **！ 设备\_信息 0xfffffa8004630690**。

**请注意**  DML 功能现已推出的 WinDbg 中，但未在 Visual Studio 或 KD。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

[ **！ Usb\_树**](-usb3kd-device-info.md)命令是此命令集的父命令。

-   [**!hub\_info**](-usb3kd-hub-info.md)
-   [**!hub\_info\_from\_fdo**](-usb3kd-hub-info-from-fdo.md)
-   [**!device\_info**](-usb3kd-device-info.md)
-   [**!device\_info\_from\_pdo**](-usb3kd-device-info-from-pdo.md)
-   [**!port\_info**](-usb3kd-port-info.md)

显示的信息[ **！ usb\_树**](-usb3kd-device-info.md)维护的 USB 3.0 集线器驱动程序的数据结构为基础的命令系列。 USB 3.0 集线器驱动程序和 USB 3.0 堆栈中的其他驱动程序有关的信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。 使用 USB 3.0 堆栈中的驱动程序的数据结构的说明，请参阅的第 2 部分[USB 调试 Windows 8 中创新](https://go.microsoft.com/fwlink/p/?LinkID=249153)视频。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






