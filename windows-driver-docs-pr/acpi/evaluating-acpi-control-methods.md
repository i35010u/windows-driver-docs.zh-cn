---
title: 评估 ACPI 控制方法
description: 评估 ACPI 控制方法
ms.assetid: 00cf7530-30e6-4ff2-8a26-1c5143413b56
keywords:
- ACPI 控制方法 WDK，评估
- ACPI 设备 WDK，评估控制方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d235720a377df453cd50abda856e30de7f3c1c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328833"
---
# <a name="evaluating-acpi-control-methods"></a>评估 ACPI 控制方法


高级配置和电源接口 (ACPI) 控制另一方法是声明和定义操作，以查询和配置系统硬件的软件。 ACPI 兼容系统提供了少量的控制方法。 控制方法是编写在 ACPI 源语言 (ASL)、 ASL 编译器编译到 ACPI 机器语言 (AML)、 从系统固件加载到 ACPI 名称空间，以及解释 ACPI 驱动程序。

内核模式设备驱动程序符合要求的内核模式驱动程序框架 (KMDF) 为其加载它。 对于在 ACPI 枚举设备的设备堆栈中加载的驱动程序，ACPI 驱动程序始终是创建和运行的是 PDO 设备堆栈中的总线驱动程序。 此功能包括评估子对象的后代的父设备支持的控制方法。

驱动程序通过发送以下项之一来评估控制方法[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)到设备的请求。

-   [**IOCTL\_ACPI\_EVAL\_METHOD**](https://msdn.microsoft.com/library/windows/hardware/ff536148)

    此请求以同步方式计算支持的请求发送到设备的控制方法。 若要使用此 IOCTL，设备的驱动程序提供了输入和输出的方法参数缓冲区，一种方法，并等待完成请求的事件对象的名称。 方法必须是请求发送到设备的 ACPI 命名空间中的直接子对象。

-   [**IOCTL\_ACPI\_异步\_EVAL\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff536145)

    此请求以异步方式计算支持的请求发送到设备的控制方法。 若要使用此 IOCTL，驱动程序，为设备提供输入和输出的方法参数缓冲区，方法的名称和一个*IoCompletion*例程较低级别的所有驱动程序已完成请求后，I/O 管理器会立即调用。 方法必须是请求发送到设备的 ACPI 命名空间中的直接子对象。

-   [**IOCTL\_ACPI\_EVAL\_METHOD\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536149)

    此请求以同步方式计算支持的设备或设备的代子对象的控制方法为将请求发送。 若要使用此 IOCTL，设备的驱动程序提供了输入和输出方法参数缓冲区、 路径和该设备，并等待完成请求的事件对象的 ACPI 命名空间中的控制方法的名称。

-   [**IOCTL\_ACPI\_ASYNC\_EVAL\_METHOD\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536146)

    此请求的异步计算结果支持的设备或设备的代子对象的控制方法为将请求发送。 若要使用此 IOCTL，驱动程序，为设备提供输入和输出方法参数缓冲区、 路径和该设备，在 ACPI 命名空间中的控制方法的名称和一个*IoCompletion*毕竟 I/O 管理器调用的例程较低级别的驱动程序已完成请求。

有关如何以同步方式评估 ACPI 控制方法的详细信息，请参阅[评估 ACPI 控件方法以同步方式](evaluating-acpi-control-methods-synchronously.md)。 有关如何以异步方式评估 ACPI 控制方法的详细信息，请参阅[ **IOCTL\_ACPI\_异步\_EVAL\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff536145)和[**IOCTL\_ACPI\_异步\_EVAL\_方法\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536146)。

要计算的不是设备的直接子对象的控制方法的设备的驱动程序，该驱动程序必须提供的路径和名称的设备的 ACPI 命名空间中的方法。 为了获得的路径和名称的子对象的设备，Windows 支持[ **IOCTL\_ACPI\_枚举\_子级**](https://msdn.microsoft.com/library/windows/hardware/ff536147)请求，该设备的驱动程序可以使用以下枚举：

-   设备和其直接子设备。

-   该设备，其所有子代子设备。

-   设备包括的 ACPI 命名空间中提供的名称的子代的子对象具体而言，控制方法。

有关如何枚举设备和设备的命名空间中的方法的信息，请参阅[枚举子设备和控制方法](enumerating-child-devices-and-control-methods.md)。

有关系统提供的宏，驱动程序可以用来帮助评估控制方法的信息，请参阅[控制方法的宏](control-method-macros.md)。

有关 ACPI 设备、 控制方法和命名空间的详细信息，请参阅[高级配置和电源接口规范](https://go.microsoft.com/fwlink/p/?linkid=866846)。
