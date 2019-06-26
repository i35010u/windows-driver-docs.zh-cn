---
title: 同步评估 ACPI 控制方法
description: 同步评估 ACPI 控制方法
ms.assetid: 3fd8f7bd-bfae-4846-8051-3a0023d565e4
keywords:
- ACPI 控制方法 WDK，以同步方式评估
- ACPI 控制方法 WDK，输入的缓冲区结构
- ACPI 控制方法 WDK，SendDownStreamIrp 代码示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c5a09a840543b8d122a3cc5ba2fae0279e023a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355836"
---
# <a name="evaluating-acpi-control-methods-synchronously"></a>同步评估 ACPI 控制方法


设备驱动程序可以使用以下设备控制请求以同步方式对设备的 ACPI 命名空间中定义的控制方法进行评估：

-   [**IOCTL\_ACPI\_EVAL\_METHOD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)

    此请求的计算结果是将请求发送到设备的 ACPI 命名空间中的直接子对象的控制方法。

-   [**IOCTL\_ACPI\_EVAL\_METHOD\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)

    此请求以同步方式计算支持的设备或设备的代子对象的控制方法为将请求发送。

[Windows ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)，Acpi.sys，处理这些请求代表系统描述表中指定的设备[ACPI BIOS](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-bios)。 这些请求可由内核模式设备驱动程序符合的要求[内核模式驱动程序框架 (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)或[Windows 驱动程序模型 (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)。 从 Windows 8 开始，符合的要求的用户模式设备驱动程序[用户模式驱动程序框架 (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)可以使用这些请求。

例如，WDM 驱动程序将执行以下一系列操作，使用这些 Ioctl 之一：

1.  调用[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)要生成请求。

2.  调用[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)发送关闭设备堆栈请求。

3.  等待 I/O 管理器，以指示驱动程序的较低级驱动程序已完成请求。

4.  检查请求的状态。

5.  检查输出自变量的有效性。

6.  处理向驱动程序返回的输出自变量。

7.  完成请求。

若要生成请求，驱动程序调用**IoBuildDeviceIoControlRequest**并提供以下参数：

-   *IoControlCode*设置为**IOCTL\_ACPI\_EVAL\_方法**或者**IOCTL\_ACPI\_EVAL\_方法\_例如**。

-   *DeviceObject*设置为指向该设备的物理设备对象 (PDO) 的指针。

-   *InputBuffer*设置为指向取决于输入参数来传递到控制方法的类型的输入的缓冲区结构的指针。 ACPI 驱动程序支持不采用输入的参数，采用单个整数，需要为 ASCII 字符串，或需要输入参数的自定义数组的方法。 有关受支持的输入的缓冲区结构的详细信息，请参阅[控制方法输入缓冲区结构](control-method-input-buffer-structures.md)。

-   *InputBufferLength*设置为，以字节为单位，由提供的输入缓冲区的大小*InputBuffer*。

-   *OutputBufferLength*提供的大小，以字节为单位，由提供的输出缓冲区*OutputBuffer*。

-   *InternalDeviceIoControl*设置为**FALSE**。

-   *事件*设置为指向调用方分配并初始化事件对象的指针。 该驱动程序等待，直到 I/O 管理器通知此事件表示的较低级驱动程序已完成请求。

-   *OutputBuffer*提供一个指向[ **ACPI\_EVAL\_输出\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)结构，其中包含从输出自变量控制方法。 输出自变量是特定于给定的控件方法。 驱动程序返回任何输出，它必须分配足够大以保存所有输出参数的缓冲区。

-   *IoStatusBlock*设置为[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)结构。 这会返回请求的较低级驱动程序所设置的状态。

有关如何评估则不使用输入的参数的控制方法的代码示例，请参阅[评估控制方法而无需输入参数](evaluating-a-control-method-without-input-arguments.md)。

有关如何评估使用输入的参数的控制方法的代码示例，请参阅[评估该采用输入参数的控制方法](evaluating-a-control-method-that-takes-input-arguments.md)。
