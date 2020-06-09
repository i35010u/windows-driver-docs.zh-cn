---
title: usb3kd ucx_controller_list
description: Ucx_controller_list usb3kd 命令显示有关计算机上的所有 USB 3.0 主机控制器的信息。 显示基于 UcxVersion 维护的数据结构。
ms.assetid: 57565A2A-A409-46CE-B7F9-F1CD521960E5
keywords:
- usb3kd ucx_controller_list Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.ucx_controller_list
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 213f659f34a08f66eaca27e4bc1f25da1ae164c3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534170"
---
# <a name="usb3kducx_controller_list"></a>！ usb3kd ucx \_ 控制器 \_ 列表


[**！ Usb3kd. ucx \_ controller \_ list**](-usb3kd-device-info.md)命令显示有关计算机上的所有 USB 3.0 主机控制器的信息。 此显示基于 USB 主机控制器扩展驱动程序 *（Ucx）* 所维护的数据结构。

```dbgcmd
!usb3kd.ucx_controller_list
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


以下屏幕截图显示[**！ ucx \_ controller \_ list**](-usb3kd-device-info.md)命令的输出。

![\- \- 显示 ucx 控制器设备和终结点的！ ucx controller list 命令的输出](images/ucxcontrollerlist01.png)

输出显示有一个 USB 3.0 主机控制器，它由以[**！ ucx \_ 控制器**](-usb3kd-ucx-controller.md)开头的行表示。 你可以看到两个设备已连接到控制器，并且每个设备都有四个终结点。

输出使用[调试器标记语言（DML）](debugger-markup-language-commands.md)来提供链接。 这些链接执行命令，以获得有关各个设备或终结点的详细信息。 例如，可以通过单击某个[**！ ucx \_ 终结点**](-usb3kd-ucx-endpoint.md)链接获取有关终结点的详细信息。 作为单击链接的替代方法，可以输入命令。 例如，若要查看第二个设备的第一个终结点的信息，可以输入命令 **！ ucx \_ 终结点 0xfffffa8003694860**。

**注意**   DML 功能在 WinDbg 中可用，但在 Visual Studio 或 KD 中不可用。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd

<a name="remarks"></a>注解
-------

[**！ Ucx \_ controller \_ list**](-usb3kd-device-info.md)命令是此命令集的父命令。

-   [**！ ucx \_ 控制器**](-usb3kd-ucx-controller.md)
-   [**！ ucx \_ 设备**](-usb3kd-ucx-device.md)
-   [**！ ucx \_ 终结点**](-usb3kd-ucx-endpoint.md)

USB 主机控制器扩展驱动程序 *（Ucx）* 提供 usb 3.0 集线器驱动程序与 usb 3.0 主机控制器驱动程序之间的抽象层。 扩展驱动程序具有其自己的主机控制器、设备和终结点的表示形式。 [**！ Ucx \_ 控制器 \_ 列表**](-usb3kd-device-info.md)系列中的命令的输出基于扩展驱动程序所维护的数据结构。 有关 USB 主机控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序的详细信息，请参阅[Usb 驱动程序堆栈体系结构](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)。 有关 USB 3.0 堆栈中的驱动程序所使用的数据结构的说明，请参阅[Windows 8 视频中 USB 调试革新](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P)的第2部分。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






