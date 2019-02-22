---
title: usb3kd.ucx_controller_list
description: Usb3kd.ucx_controller_list 命令显示计算机上的所有 USB 3.0 主机控制器的信息。 显示基于由 UcxVersion.sys 维护的数据结构。
ms.assetid: 57565A2A-A409-46CE-B7F9-F1CD521960E5
keywords:
- usb3kd.ucx_controller_list Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller_list
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 40beff4b1785125f3cf95ca80639b8b7bd2ea60e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555660"
---
# <a name="usb3kducxcontrollerlist"></a>!usb3kd.ucx\_controller\_list


[ **！ Usb3kd.ucx\_控制器\_列表**](-usb3kd-device-info.md)命令的计算机上显示有关所有 USB 3.0 主机控制器的信息。 显示基于 USB 主控制器扩展驱动程序所维护的数据结构 (Ucx*版本*.sys)。

```dbgcmd
!usb3kd.ucx_controller_list
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


下面的屏幕截图显示的输出[ **！ ucx\_控制器\_列表**](-usb3kd-device-info.md)命令。

![输出 ！ ucx\-控制器\-列表命令显示 ucx 控制器设备和终结点](images/ucxcontrollerlist01.png)

输出显示有一个 USB 3.0 主控制器，由开头的行[ **！ ucx\_控制器**](-usb3kd-ucx-controller.md)。 您可以看到两个设备已连接到控制器和每个设备有四个终结点。

输出会使用[使用调试器标记语言 (DML)](debugger-markup-language-commands.md)提供链接。 链接执行命令来提供有关单个设备或终结点的详细的信息。 例如，可以通过单击之一来获取有关终结点的详细的信息[ **！ ucx\_终结点**](-usb3kd-ucx-endpoint.md)链接。 作为单击的链接的替代方法，你可以输入命令。 例如，若要查看有关第一个终结点的另一台设备的信息，可以输入命令 **！ ucx\_终结点 0xfffffa8003694860**。

**请注意**  DML 功能现已推出的 WinDbg 中，但未在 Visual Studio 或 KD。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

[ **！ Ucx\_控制器\_列表**](-usb3kd-device-info.md)命令是此命令集的父命令。

-   [**!ucx\_controller**](-usb3kd-ucx-controller.md)
-   [**!ucx\_device**](-usb3kd-ucx-device.md)
-   [**!ucx\_endpoint**](-usb3kd-ucx-endpoint.md)

USB 主控制器扩展驱动程序 (Ucx*版本*.sys) 提供的 USB 3.0 集线器驱动程序和 USB 3.0 主机之间的抽象层，控制器驱动程序。 扩展驱动程序具有其自己的主机控制器、 设备和终结点的表示形式。 中的命令的输出[ **！ ucx\_控制器\_列表**](-usb3kd-device-info.md)系列基于由扩展驱动程序维护的数据结构。 有关 USB 主控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。 使用 USB 3.0 堆栈中的驱动程序的数据结构的说明，请参阅的第 2 部分[USB 调试 Windows 8 中创新](https://go.microsoft.com/fwlink/p/?LinkID=249153)视频。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






