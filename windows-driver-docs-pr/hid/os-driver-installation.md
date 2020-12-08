---
title: OS 驱动程序安装
description: 由供应商用来控制 Microsoft 提供的键盘和鼠标类安装程序安装设备的方式的类特定 INF 文件项。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2611b06a19027579ddf7ad188581b62efef38ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838913"
---
# <a name="os-driver-installation"></a>OS 驱动程序安装


本部分介绍了由供应商用来控制 Microsoft 提供的键盘和鼠标类安装程序在 Microsoft Windows 2000 和更高版本下安装设备的方式的以下类特定 INF 文件条目

:

[INF DDInstall.MigrateToDevNode 节](inf-ddinstall-migratetodevnode-section.md)

[INF SharedDriver 条目](inf-shareddriver-entry.md)

[INF PS2 \_ 指令. NoInterruptInit. Bioses 部分](inf-ps2-inst-nointerruptinit-bioses-section.md)

[INF PS2 \_ 指令. NoInterruptInit 部分](inf-ps2-inst-nointerruptinit-section.md)

有关具体示例，请参阅 msmouse 中的这些 INF 文件条目的用法-用于键盘和鼠标设备安装程序类的 Microsoft 提供的 INF 文件。

## <a name="general-rules-for-ps2-keyboards-and-mice"></a>PS/2 键盘和鼠标的一般规则


对于通过 PS/2 兼容控制器连接的每个内部/集成设备，Microsoft Windows 操作系统使用 ACPI 来构造设备的设备标识字符串列表。 即插即用管理器使用这些设备标识字符串将设备与 INF 文件相匹配。 即插即用设备字符串分为以下几种类型：

-   单个唯一设备 ID (通常只是硬件 Id 列表中的第一个 ID) 
-   硬件 Id 的排序列表
-   兼容 Id 的排序列表

即插即用管理器尝试将设备与 INF 文件进行匹配时，始终使用列表中的所有标识符，但它首先尝试使用最特定的标识符。 这样，安装软件就可以按照其适用性顺序为驱动程序提供首选项，这些驱动程序提供的驱动程序位于优先级列表的顶部。

为了找到驱动程序匹配项，安装程序会将设备的硬件 Id 和兼容 Id (与设备的父总线驱动程序报告的 id 相比较) 到计算机上的 INF 文件中列出的硬件 Id 和兼容 Id。 如果安装程序找到多个匹配项，则会为每个可能的驱动程序匹配分配 "rank"。 排名数字越低，驱动程序的匹配程度越高。

为了实现上述方案，ACPI 应报告以下内容：

一个或多个硬件 Id，用于标识固件和/或硬件型号。 ACPI 规范 V 5.0) 中定义的 HWID (的格式如下所示：

-   ACPI \\ 即使 \_ VVVV&DEV \_ dddd&子系统 \_ ssssssss&REV \_ rrrr
-   ACPI \\ 即使 \_ VVVV&DEV \_ dddd&子系统 \_ ssssssss
-   ACPI \\ 即使 \_ VVVV&DEV \_ dddd&REV \_ rrrr
-   ACPI \\ 即使 \_ VVVV&DEV \_ dddd&CLS \_ cccc&SUBCLS \_ nnnn&PI \_ pp
-   ACPI \\ 即使 \_ VVVV&DEV \_ dddd
-   ACPI \\ vvvdddd
-   ACPI \\ vvvvdddd

一个兼容的 ID，该 ID 允许操作系统加载泛型类驱动程序。 键盘和鼠标 Inf 中已列出了这些泛型 Id。

具有格式正确的 PS/2 键盘硬件 ID 的系统示例如下所示：

-   硬件 ID： ACPI \\ MSF0001;
-   兼容 ID： \* PNP0303

说明：

-   Windows 允许旧 (例如，ACPI 4.0) 样式 ACPI 硬件 Id，但更倾向于它们始终标识唯一的键盘或鼠标设备。
-   Windows 硬件认证工具包包括以下要求 (PS2UniqueHWID) 。 在移动计算元素上通过 PS/2 嵌入键盘和鼠标的系统制造商必须确保唯一的硬件 ID。 唯一的硬件 ID 必须是一种格式，该格式允许 Windows 更新 (WU) 标识设备，并为其加载正确的驱动程序。 此 Windows 8 徽标要求适用于 x86/64 移动系统， (ARM 系统上不支持 PS/2) 

有关更多详细信息，请参阅 MSDN 白皮书，其中标题为 "便携式计算机上的 PS/2 输入设备的硬件 Id"。

 

 




