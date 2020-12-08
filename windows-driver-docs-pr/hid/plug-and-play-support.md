---
title: 即插即用支持
description: 本部分介绍通用串行总线上的枚举过程。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c87574ffa8dfa09605f29ecf08de83f16848566
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820345"
---
# <a name="plug-and-play-support"></a>即插即用支持


本部分介绍通用串行总线上的枚举过程。

将设备插入到基于 Windows 的计算机时，Windows USB stack 会枚举设备，从设备中提取详细信息，包括设备的接口描述符 (或描述符) ，然后为设备生成一组硬件 Id 和兼容 Id。

有关 USB 硬件 Id 的完整列表，请参阅设备安装下的 "设备标识字符串" 部分。

以下各节中的示例说明了两种方案：

-   单个接口 USB 设备的 USB Id
-   多接口 (复合) USB 设备的 USB Id

*示例1：单接口 HID USB 设备*

此示例演示如何在运行 Windows 2000 或 Windows XP 的系统上为单接口 USB 设备生成硬件 Id 和兼容 Id。

当 USB 堆栈最初枚举设备时，USBHUB 驱动程序将从设备描述符中提取 **idVendor**、 **idProduct** 和 **bcdDevice** 。 这三个字段合并在一起以生成 USB 硬件 ID。 请注意，供应商、设备和修订号始终以十六进制格式存储。

设备的兼容 ID 的生成更复杂。 类代码、子类代码和协议代码取决于接口描述符的 **bInterfaceClass**、 **bInterfaceSubClass** 和 **bInterfaceProtocol**。 这些值是两位数的十六进制格式。

**注意**  如果您提供的是 INF，则您的硬件标识符应与下表的左侧列中的 **粗体** 标识符相匹配。  (应避免使用正确列中列出的兼容标识符。 ) 

 

**硬件标识符**：兼容标识符

USB \\ Vid \_ Xxxx&Pid \_ yyyy&Rev \_ zzzz * * * * *： USB \\ 类 \_ aa&子类 \_ bb&Prot \_ cc

USB \\ Vid \_ Xxxx&Pid \_ yyyy * * * *： usb \\ 类 \_ aa&子类 \_ bb

： USB \\ 类 \_ aa


 

*示例2：多个接口/函数 HID USB 设备 (复合设备)*

具有多个功能的 USB 设备称为复合设备。 此示例演示如何为 Windows 上的合成 USB 设备生成硬件 Id 和兼容 Id。 将新的 USB 复合设备插入运行 Windows 的计算机系统时，USBHUB 驱动程序 (PDO 创建一个物理设备对象) 并通知操作系统其子设备集已更改。 查询用于与新 PDO 关联的硬件 Id 的集线器驱动程序之后，系统会搜索相应的 INF 文件以查找标识符匹配项。 如果供应商选择只为整个设备加载一个驱动程序 (即，不使用复合设备驱动程序) 并使用该驱动程序对软件中的所有接口进行多路复用，则供应商应指定硬件 ID 匹配，以防止操作系统拾取 (USB 复合) 的较低排名匹配 \\ 。

**注意**  如果您提供的是 INF，则您的硬件标识符应与下表的左侧列中的 **粗体** 标识符相匹配。  (应避免使用正确列中列出的兼容标识符。 ) 

 

**硬件标识符**：兼容标识符

USB \\ Vid \_ Xxxx&Pid \_ yyyy&Rev \_ zzzz * * * * *： USB \\ 类 \_ aa&子类 \_ bb&Prot \_ cc

USB \\ Vid \_ Xxxx&Pid \_ yyyy * * * *： usb \\ 类 \_ aa&子类 \_ bb

： USB \\ 类 \_ aa

： USB \\ 复合


 

但是，如果找不到硬件匹配项，则 Windows 即插即用利用 USB \\ 组合标识符将 Usb 通用父驱动程序加载 (USBCCGP) 。 然后，通用父驱动程序会为每个接口创建一组单独的 PDOs (每个接口) 为复合设备的每个接口使用一组单独的硬件 Id。 以下部分显示子 PDOs 的硬件 Id 格式。

若要为每个接口的 PDO 生成硬件 Id 集，USBCCGP 驱动程序会将接口号追加 (这是从零开始的十六进制值，) 到硬件 ID 的结尾。

类代码、子类代码和协议代码分别由接口描述符中的 **bInterfaceClass**、 **bInterfaceSubClass** 和 **bInterfaceProtocol** 字段决定。 这些值是两位数的十六进制格式。

**注意**  如果你正在提供 INF，若要加载驱动程序或提供友好的设备名称，你的硬件标识符应与下表左列中的 **粗体** 标识符相匹配。  (应避免使用正确列中列出的兼容标识符。 ) 

 

**硬件标识符**：兼容标识符

USB \\ Vid \_ Xxxx&Pid \_ yyyy&REV \_ zzzz&MI \_ ww * * * *： USB \\ 类 \_ aa&子类 \_ bb&Prot \_ cc

USB \\ Vid \_ Xxxx&Pid \_ yyyy&MI \_ ww * * * *： USB \\ 类 \_ aa&子类 \_ bb

： USB \\ 类 \_ aa


 

 

 




