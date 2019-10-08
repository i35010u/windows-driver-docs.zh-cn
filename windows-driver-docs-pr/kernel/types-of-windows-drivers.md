---
title: Windows 驱动程序的类型
description: Windows 驱动程序的类型
ms.assetid: e6696c6b-2d3c-473c-9f46-576fe0c40496
keywords:
- Windows 驱动程序 WDK，类型
- 驱动程序 WDK，类型
- 内核模式驱动程序 WDK，类型
- 最高层驱动程序 WDK
- 中间驱动程序 WDK 内核
- 最低级别驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: d348634821c1b675c388c529fe845e20f8c7575a
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007654"
---
# <a name="types-of-windows-drivers"></a>Windows 驱动程序的类型





Microsoft Windows 驱动程序有两种基本类型：

-   *用户模式驱动程序*在用户模式下执行，通常在 Win32 应用程序和内核模式驱动程序或其他操作系统组件之间提供接口。

    例如，在 Windows Vista 中，所有打印机驱动程序都在用户模式下执行。 有关打印机驱动程序组件的详细信息，请参阅[打印简介](https://docs.microsoft.com/windows-hardware/drivers/print/introduction-to-printing)。

-   *内核模式驱动程序*作为执行程序的一部分在内核模式下执行，包括管理 i/o、即插即用内存、进程和线程、安全性等的内核模式操作系统组件。 内核模式驱动程序通常是分层的。 通常，较高级别的驱动程序通常会从应用程序接收数据、筛选数据，并将其传递给支持设备功能的较低级别的驱动程序。

    某些内核模式驱动程序也是*WDM 驱动程序*，它们符合[Windows 驱动模型](windows-driver-model.md)（WDM）。 所有 WDM 驱动程序都支持即插即用和电源管理。 WDM 驱动程序跨 Windows 98/Me 和 Windows 2000 及更高版本的操作系统与源兼容（但不兼容二进制兼容）。

    与操作系统本身一样，内核模式驱动程序实现为具有一组定义完善的必需功能的离散模块化组件。 所有内核模式驱动程序都提供一组系统定义的[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)。

下图将内核模式驱动程序划分为多个类型。

![阐释内核模式驱动程序类型的关系图](images/1drvlyrs.png)

如图所示，驱动程序堆栈中有三种基本类型的内核模式驱动程序：最高级别的、中级和最低级别。 每种类型仅在结构上略有不同，但功能明显不同：

1.  *最高层驱动程序*。 最高级别的驱动程序包括支持文件系统的文件系统驱动程序（FSDs），例如：

    -   NTFS

    -   文件分配表（FAT）

    -   CD-ROM 文件系统（CDFS）

    最高层驱动程序始终依赖于底层的底层驱动程序的支持，如中间级别函数驱动程序和最低级别的硬件总线驱动程序。

2.  *中间驱动程序*，如虚拟磁盘、镜像或特定于设备类型的*类驱动程序*。 中间驱动程序依赖底层驱动程序的支持。 中间驱动程序会进一步细分，如下所示：

    -   [*函数驱动程序*](function-drivers.md)控制 i/o 总线上的特定外围设备。

    -   [*筛选器驱动*](filter-drivers.md)程序将自身插入到功能驱动程序的上方或下方。

    -   *软件总线驱动程序*提供一组仍在更高级别的类、函数或筛选器驱动程序可以附加到的子设备。

        例如，用来控制包含一组异类设备的多功能适配器的驱动程序是软件总线驱动程序。

    -   任何系统提供的用于导出系统定义的类/miniclass 接口的*类驱动程序*实际上是具有一个或多个链接的*miniclass 驱动程序*（有时称为*微型驱动程序*）的中间驱动程序。 每个链接类/微型驱动程序对提供的功能与函数驱动程序或软件总线驱动程序的功能等效。

3.  *最低级别的驱动程序*控制外围设备连接到的 i/o 总线。 最低级别的驱动程序不依赖于较低级别的驱动程序。

    -   硬件[*总线驱动程序*](bus-drivers.md)由系统提供，通常控制动态配置的 i/o 总线。

        硬件总线驱动程序与即插即用 manager 配合使用，以配置和重新配置系统硬件资源，这适用于连接到驱动程序控制的 i/o 总线的所有子设备。 这些硬件资源包括设备内存和中断请求（Irq）的映射。 （硬件总线驱动程序归类 Windows 2000 之前的基于 Windows NT 的操作系统版本中提供的某些功能。）

    -   直接控制物理设备的*传统驱动*程序是最低级别的驱动程序。

 

 




