---
title: 评估采用输入参数的控制方法
description: 评估采用输入参数的控制方法
ms.assetid: 3a4be8a8-0906-4d38-bf6d-f245e6ae236a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 365c9511abe7eea29de2857cc6c86cbb2812d011
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826181"
---
# <a name="evaluating-a-control-method-that-takes-input-arguments"></a>评估采用输入参数的控制方法


为了同步计算采用输入参数的控制方法，设备的驱动程序将[**ioctl\_acpi\_eval\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)请求或[**ioctl\_acpi\_eval\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)请求到设备。 [同步评估 ACPI 控制方法](evaluating-acpi-control-methods-synchronously.md)中介绍了这两个请求的一般过程。 使用这两个请求的具体区别如下：

-   如果控制方法是设备的直接子对象，则驱动程序将\_ACPI\_EVAL\_方法请求发送 IOCTL，并提供以下输入结构之一： [**ACPI\_EVAL\_输入\_缓冲区\_简单\_整数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)、 [**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)，或[**ACPI\_EVAL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)\_\_\_的缓存输入。

-   如果控制方法是设备 ACPI 命名空间中的子对象，但不是设备的直接子对象，则驱动程序将\_ACPI\_EVAL\_方法发送 IOCTL，\_EX 请求并提供以下输入之一结构： [**ACPI\_EVAL\_输入\_缓冲区\_简单\_整数\_例如**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1_ex)， [**ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串\_例如**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)，或[**ACPI\_EVAL\_输入\_缓冲区\_复杂\_例如**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)

本主题中提供的示例*EvaluateABCDWithInputArgument*函数说明了驱动程序如何使用 IOCTL\_ACPI\_EVAL\_方法请求来计算采用单个整数输入的名为 "ABCD" 的控制方法实际.

如果输入参数是字符串或自定义数据的数组而不是整数，则对示例代码所需的更改是提供字符串输入结构或复杂输入结构，而不是整数输入结构。

此外，如果 "ABCD" 控制方法不是直接子对象，则示例代码所需的更改如下所示：

-   将 IOCTL\_ACPI\_EVAL\_方法\_EX 请求，而不是使用 IOCTL\_ACPI\_EVAL\_方法请求。

-   提供对应于输入参数类型的扩展输入结构类型（简单整数、简单字符串或复杂类型）。

*EvaluateABCDWithInputArgument*首先分配一个 ACPI\_EVAL\_输入\_缓冲区\_简单的\_整数结构*inputBuffer* ，然后将**MethodNameAsUlong**成员设置为control 方法，将**IntegerArgument**成员设置为输入整数值，并将**签名**成员设置为 ACPI\_EVAL\_输入\_缓冲区\_简单\_整数\_签名。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.IntegerArgument  =  Argument1;
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_SIGNATURE;
```

*EvaluateABCDWithInputArgument*还会将[**ACPI\_EVAL\_输出分配\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)结构*outputBuffer*，但不会设置*outputBuffer*的任何成员。

然后， *EvaluateABCDWithInputArgument*调用驱动程序提供的名为[SendDownStreamIrp](senddownstreamirp-function.md)的函数来执行以下操作：

1.  调用[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)以生成请求。

2.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将请求发送到设备堆栈中。

3.  等待 i/o 管理器通知驱动程序低级驱动程序已完成该请求。

在 i/o 管理器发出请求后， **SendDownStreamIrp**将返回该请求的信号。

尽管*EvaluateABCDWithInputArgument*中未包括，但驱动程序还应在**SendDownStreamIrp**返回后执行以下其他操作：

1.  检查**SendDownStreamIrp**返回的状态。 如果**SendDownStreamIrp**未返回状态\_成功，则驱动程序将返回，而不进行其他处理。

2.  检查输出参数的有效性。 对于包含有效输出数据的*outputBuffer* ，必须将**签名**设置为 ACPI\_EVAL\_输出\_缓冲区\_签名，**计数**必须设置为大于零。

3.  处理传回驱动程序的输出参数。

4.  调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)来完成 IOCTL\_ACPI\_EVAL\_方法请求。

以下示例中使用的 ACPI 数据结构和常量是在*Acpiioct*中定义的。

```cpp
NTSTATUS
EvaluateABCDWithInputArgument(
    IN PDEVICE_OBJECT   Pdo,
    IN ULONG            Argument1,
    OUT PULONG          ReturnStatus
    )
/*
Routine Description:
    Called to evaluate the example 'ABCD' method with a single integer input argument

Parameters:
    Pdo             - For the device.
    Argument1       - Input argument.
    ReturnStatus    - Pointer to where the status data is placed.

Return Value:
    NT Status of the operation
*/
{
 ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER  inputBuffer;
    ACPI_EVAL_OUTPUT_BUFFER                outputBuffer; 
    NTSTATUS                               status;
    PACPI_METHOD_ARGUMENT                  argument;

    .
    .
    // Omitted: bounds checking on Argument1 value.


    ASSERT( ReturnStatus != NULL );
    *ReturnStatus = 0x0;

    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.IntegerArgument  =  Argument1;
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_SIGNATURE;

    // Send the request along
    status = SendDownStreamIrp(
       Pdo,
       IOCTL_ACPI_EVAL_METHOD,
       &inputBuffer,
       sizeof(ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER),
       &outputBuffer,
       sizeof(ACPI_EVAL_OUTPUT_BUFFER)
       );

    return status;
}
```

 

 




