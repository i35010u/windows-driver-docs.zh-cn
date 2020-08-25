---
title: 同步评估 ACPI 控制方法
description: 同步评估 ACPI 控制方法
ms.assetid: 3fd8f7bd-bfae-4846-8051-3a0023d565e4
keywords:
- ACPI 控制方法 WDK，同步评估
- ACPI 控制方法 WDK，输入缓冲区结构
- ACPI 控制方法 WDK，SendDownStreamIrp 代码示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eee4e2a9794d3323bea8f9c8892e4374e21b63f9
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850231"
---
# <a name="evaluating-acpi-control-methods-synchronously"></a>同步评估 ACPI 控制方法


设备驱动程序可以使用下列设备控制请求来同步计算设备 ACPI 命名空间中定义的控制方法：

-   [**IOCTL \_ ACPI \_ EVAL \_ 方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)

    此请求将评估一个控制方法，该方法是请求发送到的设备的 ACPI 命名空间中的直接子对象。

-   [**IOCTL \_ ACPI \_ EVAL \_ 方法（ \_ EX）**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)

    此请求同步计算设备或请求发送到的设备的子代子对象所支持的控制方法。

[WINDOWS ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)Acpi.sys，代表在[ACPI BIOS](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-bios)中的系统说明表中指定的设备来处理这些请求。 这些请求可由符合 [内核模式驱动程序框架 ](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide) 要求的内核模式设备驱动程序使用 (KMDF) 或 [Windows 驱动模型 (WDM) ](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-wdm)。 从 Windows 8 开始，符合 [用户模式驱动程序框架要求 (UMDF) ](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf) 的用户模式设备驱动程序可以使用这些请求。

例如，WDM 驱动程序执行以下一系列操作来使用下列 IOCTLs 之一：

1.  调用 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 以生成请求。

2.  调用 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将请求发送到设备堆栈中。

3.  等待 i/o 管理器通知驱动程序低级驱动程序已完成该请求。

4.  检查请求的状态。

5.  检查输出参数的有效性。

6.  处理返回给驱动程序的输出参数。

7.  完成请求。

若要生成请求，驱动程序将调用 **IoBuildDeviceIoControlRequest** 并提供以下参数：

-   *IoControlCode*设置为**ioctl \_ Acpi \_ eval \_ 方法**或**ioctl \_ acpi \_ eval 方法， \_ \_ 例如**

-   *DeviceObject* 设置为指向设备 (PDO) 的物理设备对象的指针。

-   *InputBuffer* 设置为一个指向输入缓冲区结构的指针，该结构依赖于要传递给控件方法的输入参数的类型。 ACPI 驱动程序支持不采用输入参数的方法，这些方法采用单个整数、采用 ASCII 字符串或采用自定义的输入参数数组。 有关支持的输入缓冲区结构的详细信息，请参阅 [控制方法输入缓冲区结构](control-method-input-buffer-structures.md)。

-   *InputBufferLength* 设置为 *InputBuffer*提供的输入缓冲区的大小（以字节为单位）。

-   *OutputBufferLength* 提供 *OutputBuffer*提供的输出缓冲区的大小（以字节为单位）。

-   *InternalDeviceIoControl* 设置为 **FALSE**。

-   *事件* 设置为指向分配给调用方的事件对象的指针。 该驱动程序将等待，直到 i/o 管理器发出此事件的信号，指示较低级别的驱动程序已经完成了该请求。

-   *OutputBuffer* 提供指向 [**ACPI \_ EVAL \_ 输出 \_ 缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1) 的指针，该结构包含来自控制方法的输出参数。 输出参数特定于给定的控制方法。 若要使驱动程序返回任何输出，它必须分配一个足够大的缓冲区来容纳所有输出参数。

-   *IoStatusBlock* 设置为 [**IO \_ 状态 \_ 块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构。 这会返回较低级别驱动程序设置的请求的状态。

有关如何计算不采用输入参数的控制方法的代码示例，请参阅 [计算控制方法但不使用输入参数](evaluating-a-control-method-without-input-arguments.md)。

有关如何评估采用输入参数的控制方法的代码示例，请参阅 [计算采用输入参数的控制方法](evaluating-a-control-method-that-takes-input-arguments.md)。
