---
title: 打印机安装和即插即用管理器
description: 打印机安装和即插即用管理器
ms.assetid: 1edc92f1-fcd9-4af0-957d-cd7ff2e40125
keywords:
- 即插即用管理器 WDK 打印
- 重复安装检测 WDK 打印
- 检测重复的打印机安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1780be0ab9d35d0cdbe8b2aea234ceedec15884
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850297"
---
# <a name="printer-installation-and-the-plug-and-play-manager"></a>打印机安装和即插即用管理器

即插即用 manager 处理计算机的所有即插即用事件，并对所有设备都是通用的。 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-plug-and-play)中记录了即插即用管理器。 [即插即用简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-plug-and-play) 概述了即插即用安装以及各种内核模式和用户模式组件交互的方式。

## <a name="printer-installation-differences-between-windows-98me-and-windows-2000-and-later"></a>Windows 98/Me 与 Windows 2000 及更高版本之间的打印机安装差异

Windows 2000 和更高版本上的即插即用体系结构与 Windows 95/98/Me 上的体系结构不同。 最重要的区别包括：

- Windows 2000 及更高版本附带的驱动程序包含在安装操作系统时安装的文件 driver.cab 中。 此文件包含所有设备类型的所有即插即用内置驱动程序，因此用户通常不需要使用原始安装介质来安装驱动程序。

- 安装特定驱动程序需要少量用户干预或无需用户干预。 如果由 Microsoft 进行数字签名的 Windows 2000 或更高版本的驱动程序处于 driver.cab 或已在计算机上安装，即插即用将验证驱动程序的签名，并在无用户干预的情况下安装驱动程序。 这种类型的安装称为 "服务器端安装"。 如果驱动程序在系统上不可用，或未签名，或者驱动程序安装需要通过用户界面元素与用户 (进行交互) ，则即插即用恢复为客户端安装。 有关每种类型的安装的详细信息，请参阅 [设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))中的用户模式 PnP 管理器讨论。 在大多数情况下，当使用连接到该设备的新即插即用设备启动计算机时，设备已安装并可供用户登录时使用。

如果用户必须能够选择要安装的驱动程序，则可以在 [**INF ControlFlags 节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)中使用 InteractiveInstall 指令。 此指令仅可用于以下两种情况：

1. 安装定义不正确的硬件 Id 的设备。 当硬件设备的硬件 ID 损坏或硬件供应商将相同的硬件 ID 分配给两个不同的设备（硬件设计错误）时，可能会出现这种情况。

1. 为不能使用泛型类安装程序或操作系统提供的驱动程序的设备安装驱动程序。

如果硬件 Id 或兼容 Id 与 InteractiveInstall 指令一起列出，安装程序会将与这些 Id 相匹配的打印机安装推迟到客户端，因此在管理员登录之前，安装会被延迟。 系统将提示管理员安装正确的驱动程序文件。 如果两个打印机驱动程序共享同一 *设备 ID*，但需要不同的驱动程序，这会很有用。

与 Windows 2000 和更高版本不同，Windows 95/98/Me 即插即用仅当存在 (名次) 匹配的 *硬件 ID* 时才安装设备，而无需用户干预。 如果有一个 *兼容 ID* (即插即用设备的驱动程序的等级 1) 匹配，但没有匹配的硬件 id，则系统会提示用户从安装介质中选择正确的驱动程序。  (这意味着用户必须具有安装介质才能安装驱动程序。 ) 

此外，在 Windows 95/98/Me 上，当驱动程序是为多个设备编写的， (或在多个总线上的类似设备上) ，除非列出了每个可能的硬件 ID 并在 INF 文件中列出了重复的驱动程序条目，否则，将始终提示用户安装。

## <a name="duplicate-installation-detection"></a>重复的安装检测

当安装程序调用打印机类安装程序来安装打印机时，类安装程序将确定是否已手动安装打印机。 它通过查找当前安装的打印机的驱动程序和端口名称与 INF 文件中列出的完全匹配项来实现此功能。 如果类安装程序查找其驱动程序和端口名称与这两个参数匹配的已安装打印队列，则不会安装第二个打印队列，而是将其与 *devnode* 项关联。 这会阻止为同一设备创建第二个打印队列。

许多常见的打印机型号 (HP DeskJet 系列共享相同的硬件 ID，如) 。 在 Windows 95/98/Me 上，如果用户手动安装随后即插即用检测到的 DeskJet 模型，则当用户选择适当的驱动程序时，将安装第二个打印队列。 如果用户未选择驱动程序，则每次计算机重新启动时，系统都会提示他们执行此操作。

Windows 2000 和更高版本通过列出 *硬件 id* 和 *兼容 ID* 匹配的所有打印机来避免这种行为。 找到多个匹配项时，类安装程序将检查是否已存在具有相同硬件 ID 匹配项的打印队列。 如果有，即插即用管理器不会安装第二个队列。 如果不是，则硬件 ID 匹配会降级为兼容的 ID 匹配。 如果 InteractiveInstall 项中还列出了这些硬件 Id (请参阅 inf 文件的 [**Inf ControlFlags 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)) ，系统将提示用户选择一个驱动程序。
