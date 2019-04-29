---
title: 即插即用支持
description: 本部分介绍通用串行总线上枚举过程。
ms.assetid: CB3D76DB-4A96-4A19-BC1C-C9181A12B04E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43b79780964ab0a94bd066cad6d243d55a62e6d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372978"
---
# <a name="plug-and-play-support"></a>即插即用支持


本部分介绍通用串行总线上枚举过程。

当设备插入到基于 Windows 的计算机，Windows USB 堆栈枚举设备，从设备包括设备的接口描述符 （或描述符） 中提取的详细信息，然后生成一组硬件 Id 和兼容 Id设备。

有关 USB 的硬件 Id 的完整列表，请参阅设备安装下的"设备标识字符串"部分。

以下各节中的示例演示了两种方案：

-   单个接口 USB 设备的 USB Id
-   多个接口 （复合） USB 设备的 USB Id

*示例 1:单个接口 HID USB 设备*

此示例演示如何为运行 Windows 2000 或 Windows XP 的系统上的单个接口 USB 设备生成的硬件 Id 和兼容 Id。

USBHUB 驱动程序时由 USB 堆栈最初枚举设备时，将提取**idVendor**， **idProduct**，并**bcdDevice**从设备描述符。 这三个字段合并以生成 USB 硬件 id。 请注意，始终以十六进制格式存储供应商、 设备和修订号。

适用于设备的兼容 ID 的代得更复杂。 类代码、 子类代码和协议代码由接口描述符**bInterfaceClass**， **bInterfaceSubClass**，并**bInterfaceProtocol**。 这些值是两位数的十六进制格式。

**请注意**  如果你要提供 INF，硬件标识符应匹配**粗体**以下表的左侧列中的标识符。 （您应避免使用兼容的标识符的右侧列中列出。）

 

|                                        |                                      |
|----------------------------------------|--------------------------------------|
| 硬件标识符                   | 兼容的标识符               |
| **USB\\Vid\_xxxx&Pid\_yyyy&Rev\_zzzz** | USB\\Class\_aa&SubClass\_bb&Prot\_cc |
| **USB\\Vid\_xxxx&Pid\_yyyy**           | USB\\Class\_aa&SubClass\_bb          |
|                                        | USB\\类\_aa                       |

 

*示例 2:多个接口/函数 HID USB 设备 （复合设备）*

USB 设备与多个函数调用组合设备。 此示例演示如何在 Windows 上的复合 USB 设备的生成的硬件 Id 和兼容 Id。 当新的 USB 复合设备插入到运行 Windows 的计算机系统时，USBHUB 驱动程序创建一个物理设备对象 (PDO)，并通知其的子设备集已更改的操作系统。 查询的硬件 Id 与新 PDO 相关联的中心驱动程序后, 系统搜索相应的 INF 文件，查找匹配项的标识符。 如果供应商选择加载整个设备 （即，不使用复合设备驱动程序） 只是一个驱动程序和多路复用与该驱动程序软件中的所有接口，供应商应指定硬件 ID 匹配项，以防止操作系统中选取较低排名匹配 (USB\\复合)。

**请注意**  如果你要提供 INF，硬件标识符应匹配**粗体**以下表的左侧列中的标识符。 （您应避免使用兼容的标识符的右侧列中列出。）

 

|                                        |                                      |
|----------------------------------------|--------------------------------------|
| 硬件标识符                   | 兼容的标识符               |
| **USB\\Vid\_xxxx&Pid\_yyyy&Rev\_zzzz** | USB\\Class\_aa&SubClass\_bb&Prot\_cc |
| **USB\\Vid\_xxxx&Pid\_yyyy**           | USB\\Class\_aa&SubClass\_bb          |
|                                        | USB\\类\_aa                       |
|                                        | USB\\复合                       |

 

Windows 即插如果，但是，发现没有硬件匹配，将使用的 USB\\复合标识符加载通用父表 USB 驱动程序 (USBCCGP)。 泛型父驱动程序然后与一组单独的每个接口的复合设备硬件 Id 创建一组单独的 PDOs （一个用于每个接口）。 以下部分显示子 PDOs 硬件 Id 的格式。

若要生成的一套硬件 Id 对每个接口的 PDO，USBCCGP 驱动程序 （这是一个从零开始的十六进制值） 的接口号末尾追加的硬件 id。

类代码、 子类代码和协议代码由**bInterfaceClass**， **bInterfaceSubClass**，并**bInterfaceProtocol**接口的字段描述符，分别。 这些值是两位数的十六进制格式。

**请注意**  如果你要提供 INF，若要加载您的驱动程序，或提供一个友好的设备名称，硬件标识符应与**粗体**以下表的左侧列中的标识符。 （您应避免使用兼容的标识符的右侧列中列出。）

 

|                                               |                                      |
|-----------------------------------------------|--------------------------------------|
| 硬件标识符                          | 兼容的标识符               |
| **USB\\Vid\_xxxx&Pid\_yyyy&Rev\_zzzz&MI\_ww** | USB\\Class\_aa&SubClass\_bb&Prot\_cc |
| **USB\\Vid\_xxxx&Pid\_yyyy&MI\_ww**           | USB\\Class\_aa&SubClass\_bb          |
|                                               | USB\\类\_aa                       |

 

 

 




