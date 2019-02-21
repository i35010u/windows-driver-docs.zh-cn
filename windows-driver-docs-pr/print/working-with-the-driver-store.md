---
title: 使用驱动程序存储区
description: V4 打印驱动程序在驱动程序存储区，直接执行和增强的点和打印不会下载整个驱动程序包到客户端计算机，所以务必要注意在本部分中的最佳实践。
ms.assetid: 71199500-ECAD-46A8-8A9B-533DDB9783B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3467ec9e67003b21fc79a0c6f6aa84fdbee00f5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521258"
---
# <a name="working-with-the-driver-store"></a>使用驱动程序存储区


V4 打印驱动程序在驱动程序存储区，直接执行和增强的点和打印不会下载整个驱动程序包到客户端计算机，所以务必要注意在本部分中的最佳实践。

-   驱动程序二进制文件不应尝试在驱动程序中打开任何其他二进制文件。 相反，驱动程序二进制文件应使用的驱动程序属性包来封装任何公用、 专用的数据。

-   如果您要开发分开安装，驱动程序 （例如，带有的 MSI 或 setup.exe），然后在此处的打印机扩展一些建议做法：

    o 当打印机扩展应用程序注册与打印系统时，应用程序应指定命令行开关在其 AppPath 条目中，来通知 PrinterDriverID 打印系统为其启动应用程序的应用。 命令行开关也表示为其打印系统启动应用程序的操作的模式。

    o 如果打印机扩展应用程序的用户启动上下文需要不同的交换机，你可以提供这些选项中的开始菜单快捷方式，但这不是必需的。

-   如果您开发的驱动程序安装的打印机扩展应用程序，请记住，这种类型的应用程序将安装到驱动程序存储区。 并且还将注意以下：

    这些应用程序打印系统中，将自动注册，并且将使用默认命令行开关注册 o。

    o 指定其他命令行开关不支持此类应用程序。

    这些应用将启动外部打印首选项或打印机通知事件，以便创建开始菜单快捷方式，或否则允许用户启动这些应用程序上下文之外的两个事件之一是不受支持 o。

## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序开发最佳做法](v4-printer-driver-development-best-practices.md)  



