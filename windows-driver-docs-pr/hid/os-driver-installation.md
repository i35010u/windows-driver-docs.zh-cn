---
title: OS 驱动程序安装
description: 供应商可用于控制如何将 Microsoft 提供键盘和鼠标类安装程序安装设备的特定于类的 INF 文件条目。
ms.assetid: A934B1F3-01FA-4B70-92B8-9CB3EB096C89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d263ab4caaff3a32583d1b22051cc6e05c43affb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372970"
---
# <a name="os-driver-installation"></a>OS 驱动程序安装


本部分介绍一个供应商可以使用来控制如何将 Microsoft 提供键盘和鼠标类安装程序安装在 Microsoft Windows 2000 及更高版本的设备的以下特定于类的 INF 文件条目

：

[INF DDInstall.MigrateToDevNode 部分](inf-ddinstall-migratetodevnode-section.md)

[INF SharedDriver 条目](inf-shareddriver-entry.md)

[INF PS2\_Inst.NoInterruptInit.Bioses 部分](inf-ps2-inst-nointerruptinit-bioses-section.md)

[INF PS2\_Inst.NoInterruptInit 部分](inf-ps2-inst-nointerruptinit-section.md)

有关具体示例，请参阅 keyboard.inf 和 msmouse.inf-键盘和鼠标设备安装程序类的 Microsoft 提供的 INF 文件中这些 INF 文件条目的使用情况。

## <a name="general-rules-for-ps2-keyboards-and-mice"></a>Ps/2 键盘和鼠标的一般规则


为通过 ps/2 控制器连接每个内部 / 集成设备，Microsoft Windows 操作系统使用 ACPI 构造一系列设备的设备标识字符串。 插管理器使用这些设备标识字符串匹配的 INF 文件的设备。 Plug and Play 设备字符串分为以下类型：

-   单个的唯一设备 ID (通常就是在硬件 Id 列表中的第一个 ID)
-   硬件 Id 的有序列的表
-   兼容 Id 有序列的表

插管理器始终使用的所有标识符的列表中时它尝试匹配设备 INF 文件，但它先尝试使用最具体的标识符。 这允许优先顺序的适用性，具有由供应商正在顶部的优先级列表提供这些驱动程序的驱动程序的安装程序软件。

若要找不到驱动程序匹配，安装程序比较设备的硬件 Id，并在计算机上的 INF 文件中列出的硬件 Id 和兼容 Id 兼容 Id （如报告的设备的父总线驱动程序）。 如果安装程序发现多个匹配项，它将一个"等级"分配给每个可能的驱动程序匹配项。 编号越低排名，更好的匹配驱动程序可用于设备。

若要实现上面所述的方案，ACPI 应报告以下：

一个或多个硬件 Id 来标识固件和/或硬件模型。 HWID （如定义在 ACPI 规范 5.0 版） 的格式如下所示：

-   ACPI\\VEN\_vvvv&DEV\_dddd&SUBSYS\_ssssssss&REV\_rrrr
-   ACPI\\VEN\_vvvv&DEV\_dddd&SUBSYS\_ssssssss
-   ACPI\\VEN\_vvvv&DEV\_dddd&REV\_rrrr
-   ACPI\\VEN\_vvvv&DEV\_dddd&CLS\_cccc&SUBCLS\_nnnn&PI\_pp
-   ACPI\\VEN\_vvvv&DEV\_dddd
-   ACPI\\vvvdddd
-   ACPI\\vvvvdddd

若要允许操作系统加载泛型类的驱动程序的一个兼容 ID。 这些泛型 Id 已列入键盘和鼠标 Inf。

格式正确的 ps/2 键盘硬件 ID 与系统的示例如下所示：

-   硬件 ID:ACPI\\MSF0001;
-   兼容 ID:\*PNP0303

注意：

-   Windows 允许旧版 (例如 ACPI 4.0) 样式 ACPI 硬件 Id，但更适合于创建它们始终标识唯一的键盘或鼠标设备。
-   Windows 硬件认证工具包包括以下要求 (System.Fundamentals.Input.PS2UniqueHWID)。 通过 PS/2 嵌入键盘和鼠标，移动计算元素上的系统制造商必须确保唯一的硬件 id。 允许 Windows Update (WU) 来标识设备，并为其加载正确的驱动程序的格式必须是唯一的硬件 ID。 此 Windows 8 徽标要求适用于 x86/64 移动系统 （不支持 PS/2 在 ARM 系统上）

有关其他详细信息，请参阅 MSDN 白皮书标题为"便携式计算机上的 PS/2 输入设备的硬件 Id"。

 

 




