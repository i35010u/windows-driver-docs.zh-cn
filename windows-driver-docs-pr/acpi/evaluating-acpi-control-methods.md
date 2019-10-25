---
title: 评估 ACPI 控制方法
description: 评估 ACPI 控制方法
ms.assetid: 00cf7530-30e6-4ff2-8a26-1c5143413b56
keywords:
- ACPI 控制方法 WDK，评估
- ACPI 设备 WDK，评估控制方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bb5ff6dae2ca63e62f29757c93254da264fe124
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826767"
---
# <a name="evaluating-acpi-control-methods"></a>评估 ACPI 控制方法


高级配置和电源接口（ACPI）控制方法是声明和定义用于查询和配置系统硬件的操作的软件。 ACPI 兼容的系统提供一组最小的控制方法。 控制方法以 ACPI 源语言（ASL）编写，由 ASL 编译器编译为 ACPI 机器语言（AML），从系统固件加载到 ACPI 命名空间，由 ACPI 驱动程序解释。

符合内核模式驱动程序框架（KMDF）的要求的内核模式设备驱动程序。 对于在 ACPI 枚举设备的设备堆栈中加载的驱动程序，ACPI 驱动程序始终是在设备堆栈中创建和操作 PDO 的总线驱动程序。 此功能包括对作为父设备后代的子对象支持的控制方法。

驱动程序通过向设备发送以下[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求来计算控制方法。

-   [**IOCTL\_ACPI\_EVAL\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)

    此请求同步计算请求发送到的设备所支持的控制方法。 若要使用此 IOCTL，设备的驱动程序提供输入和输出方法参数缓冲区、方法的名称以及等待请求完成的事件对象。 方法必须是向其发送请求的设备的 ACPI 命名空间中的直接子对象。

-   [**IOCTL\_ACPI\_ASYNC\_EVAL\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method)

    此请求异步评估请求发送到的设备所支持的控制方法。 若要使用此 IOCTL，设备的驱动程序提供输入和输出方法参数缓冲区、方法的名称以及 i/o 管理器在所有较低级别的驱动程序完成后调用的*IoCompletion*例程。 方法必须是向其发送请求的设备的 ACPI 命名空间中的直接子对象。

-   [**IOCTL\_ACPI\_EVAL\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)

    此请求同步计算设备或请求发送到的设备的子代子对象所支持的控制方法。 若要使用此 IOCTL，设备的驱动程序提供输入和输出方法参数缓冲区、设备 ACPI 命名空间中的控制方法的路径和名称，以及等待请求完成的事件对象。

-   [**IOCTL\_ACPI\_ASYNC\_EVAL\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex)

    此请求异步计算设备或请求发送到的设备的子代子对象所支持的控制方法。 若要使用此 IOCTL，设备的驱动程序提供输入和输出方法参数缓冲区、设备 ACPI 命名空间中的控制方法的路径和名称，以及在所有较低级别的驱动程序之后，i/o 管理器调用的*IoCompletion*例程已完成该请求。

有关如何同步评估 ACPI 控制方法的详细信息，请参阅[同步评估 Acpi 控制方法](evaluating-acpi-control-methods-synchronously.md)。 有关如何以异步方式评估 ACPI 控制方法的详细信息，请参阅[**ioctl\_acpi\_ASYNC\_EVAL\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method)和[**ioctl\_acpi\_异步\_EVAL\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_async_eval_method_ex).

若要让设备的驱动程序评估不是设备的直接子对象的控制方法，驱动程序必须在设备的 ACPI 命名空间中提供该方法的路径和名称。 为了帮助获取设备的子对象的路径和名称，Windows 支持[**IOCTL\_ACPI\_ENUM\_子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children)请求，设备的驱动程序可以使用该请求来枚举以下内容：

-   设备及其直接子设备。

-   设备及其所有子代子设备。

-   设备 ACPI 命名空间中提供的名称的子代子对象，其中包括控制方法。

有关如何枚举设备的命名空间中的设备和方法的信息，请参阅[枚举子设备和控制方法](enumerating-child-devices-and-control-methods.md)。

有关驱动程序可用于帮助评估控制方法的系统提供宏的信息，请参阅[控制方法宏](control-method-macros.md)。

有关 ACPI 设备、控制方法和命名空间的详细信息，请参阅[高级配置和电源接口规范](https://go.microsoft.com/fwlink/p/?linkid=866846)。
