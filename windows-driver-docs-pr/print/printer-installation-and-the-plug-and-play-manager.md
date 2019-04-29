---
title: 打印机安装和即插即用管理器
description: 打印机安装和即插即用管理器
ms.assetid: 1edc92f1-fcd9-4af0-957d-cd7ff2e40125
keywords:
- 插 manager WDK 打印
- 重复安装检测 WDK 打印
- 检测重复打印机安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ac8f4a73c0c3acf6f6e67b20f9ef697ed3c8e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384607"
---
# <a name="printer-installation-and-the-plug-and-play-manager"></a>打印机安装和即插即用管理器





插管理器处理的计算机的所有即插事件，并是通用的所有设备。 插管理器中记录了[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)。 [介绍插入并播放](https://msdn.microsoft.com/library/windows/hardware/ff548102)和各种内核模式和用户模式组件如何交互的插安装概述。

### <a href="" id="printer-installation-differences-between-windows-98-me-and-windows-200"></a>Windows 98 的打印机安装差异 / Me 和 Windows 2000 及更高版本

Windows 2000 及更高版本的插体系结构不同于在 Windows 95/98/me 上 最大的区别是：

-   Windows 2000 和更高版本附带的驱动程序包含在文件中，driver.cab，安装操作系统时安装。 此文件包含所有插现成驱动程序的所有类型的设备，因此用户通常不需要原始安装介质安装驱动程序。

-   安装特定驱动程序需要很少或没有用户干预。 如果 Windows 2000 或更高版本由 Microsoft 进行数字签名的驱动程序位于 driver.cab 或已在计算机上安装即插验证驱动程序的签名并安装驱动程序，而无需用户干预。 此类型的安装称为服务器端的安装。 如果该驱动程序不可用的系统上，或未签名，或驱动程序安装要求 （通过用户界面元素） 的用户交互，插将恢复到客户端安装。 有关每种类型的安装详细信息，请参阅中的用户模式即插即用管理器的讨论[设备安装组件](https://msdn.microsoft.com/library/windows/hardware/ff541277)。 在大多数情况下，当有新的即插设备连接到它，启动计算机时设备将已安装并准备好在用户登录时使用。

如果用户必须能够选择要安装的驱动程序，则可以使用中的 InteractiveInstall 指令[ **INF ControlFlags 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546342)。 只有在以下两种情况下，可以使用此指令：

1.  若要安装不正确定义的硬件 Id 的设备。 硬件设备都有一个损坏的硬件 ID，或者硬件供应商将相同的硬件 ID 分配给两个不同的设备，这是硬件设计中的错误时，就可能出现此问题。

2.  若要安装的设备，不能使用泛型类安装程序的驱动程序或驱动程序随操作系统一起提供。

如果使用 InteractiveInstall 指令列出了硬件 Id 或兼容 Id，安装程序将推迟安装的打印机匹配的客户端，这些 Id，以便安装推迟到以管理员身份登录。 系统会提示管理员安装正确的驱动程序文件。 如果两个打印机驱动程序共用同一个这很有用*设备 ID*，但需要不同的驱动程序。

与 Windows 2000 及更高版本，Windows 95/98/我 Plug and Play 安装即用设备而无需用户干预才*硬件 ID* (级别 0) 匹配。 当没有*兼容 ID*插设备，但没有硬件 ID 匹配项，用户的驱动程序 (级别 1) 匹配项系统提示您选择正确的驱动程序从安装媒体。 （这意味着用户必须具有安装介质，才能安装驱动程序。）

此外在 Windows 95/98/我，针对多个设备 （或多个总线上的类似设备），写入驱动程序时是始终提示用户输入安装如果只列出兼容 ID，除非每个可能的硬件 ID 列出使用重复的驱动程序INF 文件中的条目。

### <a name="duplicate-installation-detection"></a>重复安装检测

当安装程序调用要安装打印机的打印机类安装程序时，类安装程序将确定是否已手动安装打印机。 通过查找当前安装的打印机的驱动程序和端口名称和 INF 文件中列出的内容之间的完全匹配项来执行此操作。 如果其驱动程序类安装程序将查找已安装的打印队列，并且端口名称匹配这两个参数，它不会安装第二个打印队列，但改为将其与*devnode*条目。 这可以防止创建同一设备的第二个打印队列。

许多流行的打印机模型共享相同的硬件 ID （例如的 HP DeskJet 系列）。 在 Windows 95/98/我，如果用户手动安装 DeskJet 模型随后检测到的插即用设备，第二个打印队列已安装如果用户选择适当的驱动程序。 如果用户不会选择驱动程序，然后他或她会提示为此，每次重启计算机。

Windows 2000 及更高版本列表同时使用的所有打印机，因此可避免此行为*硬件 ID*并*兼容 ID*匹配。 找到多个匹配项，当类安装程序检查是否已存在具有相同的硬件 ID 匹配项的打印队列。 如果没有，插管理器将不安装第二个队列。 如果没有，请降级硬件 ID 匹配项的一个兼容 ID 匹配项。 如果这些硬件 Id 也会列在 InteractiveInstall 条目 (请参阅[ **INF ControlFlags 部分**](https://msdn.microsoft.com/library/windows/hardware/ff546342)) 的 INF 文件中，提示用户选择的驱动程序。

 

 




