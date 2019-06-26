---
title: Windows 驱动程序的类型
description: Windows 驱动程序的类型
ms.assetid: e6696c6b-2d3c-473c-9f46-576fe0c40496
keywords:
- Windows 驱动程序 WDK，类型
- 驱动程序 WDK，类型
- 内核模式驱动程序 WDK，类型
- 最高级别的驱动程序 WDK
- 中间驱动程序 WDK 内核
- 最低级别的驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60bd4fc29d5bba51b7dea9966a06cb92d7c116b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382940"
---
# <a name="types-of-windows-drivers"></a>Windows 驱动程序的类型





有两种基本类型的 Microsoft Windows 驱动程序：

-   *用户模式驱动程序*在用户模式下执行，它们通常会提前 Win32 应用程序和内核模式驱动程序或其他操作系统组件之间的接口。

    例如，在 Windows Vista 中，所有打印机驱动程序在用户模式下都执行。 有关打印机驱动程序组件的详细信息，请参阅[简介打印](https://docs.microsoft.com/windows-hardware/drivers/print/introduction-to-printing)。

-   *内核模式驱动程序*在内核模式下执行的管理人员，其中包括管理 I/O，插内存、 进程和线程安全性，和其他操作的内核模式操作系统组件的一部分。 内核模式驱动程序通常分为几级。 通常情况下，更高级别的驱动程序通常从应用程序接收数据、 筛选数据，并将其传递到支持设备功能的较低级驱动程序。

    某些内核模式驱动程序，还有*WDM 驱动程序*，这符合[Windows 驱动程序模型](windows-driver-model.md)(WDM)。 所有 WDM 驱动程序都支持插和电源管理。 WDM 驱动程序是源兼容 （但不是二进制兼容） 跨 Windows 98 / Me 和 Windows 2000 及更高版本的操作系统。

    操作系统本身，如内核模式驱动程序将作为离散的模块化组件，有一组定义完善的所需的功能。 所有内核模式驱动程序都提供的系统定义的一套[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)。

下图将内核模式驱动程序划分为几种类型。

![说明类型的内核模式驱动程序的关系图](images/1drvlyrs.png)

如图所示，有三种基本类型的驱动程序堆栈中的内核模式驱动程序： 最高级别的、 中级和最低级别。 每个类型仅与在结构稍有但极大的功能：

1.  *最高级别的驱动程序*。 最高级别的驱动程序包括文件系统驱动程序 (FSDs) 的支持文件系统，例如：

    -   NTFS

    -   文件分配表 (FAT)

    -   CD-ROM 文件系统 (CDFS)

    最高级别的驱动程序始终依赖于基础较低级驱动程序，如中间级功能的驱动程序和最低级别的硬件总线驱动程序的支持。

2.  *驱动程序的中间*，如虚拟磁盘、 镜像或特定于设备类型*类驱动程序*。 中间驱动程序依赖于基础的较低级驱动程序的支持。 中间驱动程序被再进一步，如下所示：

    -   [*函数的驱动程序*](function-drivers.md)控制 I/O 总线上的特定外围设备。

    -   [*筛选器驱动程序*](filter-drivers.md)之上或之下功能的驱动程序插入本身。

    -   *软件总线驱动程序*提供一组子哪些仍更高级别的类、 函数或筛选器驱动程序可以将附加到自己的设备。

        例如，控制具有一组载入的异构设备的多功能适配器的驱动程序是一个软件总线驱动程序。

    -   任何系统提供*类驱动程序*，导出系统定义的类/miniclass 接口是，实际上，中间驱动程序与一个或多个链接*miniclass 驱动程序*（有时称为*微型驱动程序*)。 每个链接的类/微型驱动程序对提供等效的功能驱动程序或软件总线驱动程序的功能。

3.  *最低级别的驱动程序*控制外围设备连接到的 I/O 总线。 最低级别的驱动程序不依赖于较低级别的驱动程序。

    -   硬件[*总线驱动程序*](bus-drivers.md)系统提供，并且通常控制可动态配置 I/O 总线。

        硬件总线驱动程序适用于要配置和重新配置系统硬件资源，适用于所有子设备连接到的 I/O 总线的驱动程序控制的插管理器。 这些硬件资源包括设备内存和中断请求 (Irq) 的映射。 （硬件总线驱动程序包含一些 HAL 组件的基于 Windows NT 的操作系统早于 Windows 2000 的版本中提供的功能。）

    -   *旧式驱动程序*直接控制物理设备是最低级别的驱动程序。

 

 




