---
title: 评估采用输入参数的控制方法
description: 评估采用输入参数的控制方法
ms.assetid: 3a4be8a8-0906-4d38-bf6d-f245e6ae236a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 457a0bcf01bf1a364b1177b7da07cd87206864fc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184873"
---
# <a name="evaluating-a-control-method-that-takes-input-arguments"></a>评估采用输入参数的控制方法


为了同步计算采用输入参数的控制方法，设备的驱动程序将向设备发送 [**ioctl \_ acpi \_ eval \_ 方法**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method) 请求或 [**ioctl \_ acpi \_ eval 方法（ \_ \_ 例如**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex) 请求）。 [同步评估 ACPI 控制方法](evaluating-acpi-control-methods-synchronously.md)中介绍了这两个请求的一般过程。 使用这两个请求的具体区别如下：

-   如果该控件方法是设备的直接子对象，则驱动程序将发送 IOCTL \_ ACPI \_ EVAL \_ 方法请求并提供下列输入结构之一： [**acpi \_ eval \_ 输入 \_ 缓冲区 \_ 简单 \_ 整数**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)、 [**acpi \_ eval \_ 输入 \_ 缓冲区 \_ 简单 \_ 字符串**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)或 [**acpi \_ eval \_ 输入 \_ 缓冲区 \_ **](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)。

-   如果控制方法是设备 ACPI 命名空间中的子对象，但不是设备的直接子对象，则驱动程序将发送 IOCTL \_ ACPI \_ eval \_ 方法 \_ ex 请求，并提供以下输入结构之一： [**acpi eval 输入缓冲区 \_ \_ \_ \_ 简单 \_ 整数 \_ ex**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1_ex)、 [**acpi \_ eval \_ 输入 \_ 缓冲区 \_ 简单 \_ 字符串 \_ **](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)（例如）或[**acpi \_ eval \_ 输入 \_ 缓冲区 \_ COMPLEX \_ ex**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)

本主题中提供的示例 *EvaluateABCDWithInputArgument* 函数说明了驱动程序如何使用 IOCTL \_ ACPI \_ EVAL \_ 方法请求来评估名为 "ABCD" 的控制方法，该方法采用单个整数输入参数。

如果输入参数是字符串或自定义数据的数组而不是整数，则对示例代码所需的更改是提供字符串输入结构或复杂输入结构，而不是整数输入结构。

此外，如果 "ABCD" 控制方法不是直接子对象，则示例代码所需的更改如下所示：

-   发送 IOCTL \_ acpi \_ eval \_ 方法 \_ EX 请求，而不是 IOCTL \_ acpi \_ eval \_ 方法请求。

-   提供与输入参数类型对应的扩展输入结构类型 (简单整数、简单字符串或复杂) 。

*EvaluateABCDWithInputArgument* 首先分配一个 ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 简单 \_ 整数结构 *inputBuffer* ，然后将 **MethodNameAsUlong** 成员设置为控制方法的名称，将 **IntegerArgument** 成员设置为输入整数值，并将 **签名** 成员设置为 ACPI \_ EVAL \_ 输入 \_ 缓冲区 \_ 简单 \_ 整数 \_ 签名。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.IntegerArgument  =  Argument1;
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_SIGNATURE;
```

*EvaluateABCDWithInputArgument* 还会分配一个 [**ACPI \_ EVAL \_ 输出 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1) 结构 *outputBuffer*，但不会设置 *outputBuffer*的任何成员。

然后， *EvaluateABCDWithInputArgument*调用驱动程序提供的名为[SendDownStreamIrp](senddownstreamirp-function.md)的函数来执行以下操作：

1.  调用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 以生成请求。

2.  调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将请求发送到设备堆栈中。

3.  等待 i/o 管理器通知驱动程序低级驱动程序已完成该请求。

在 i/o 管理器发出请求后， **SendDownStreamIrp**将返回该请求的信号。

尽管 *EvaluateABCDWithInputArgument*中未包括，但驱动程序还应在 **SendDownStreamIrp** 返回后执行以下其他操作：

1.  检查 **SendDownStreamIrp** 返回的状态。 如果 **SendDownStreamIrp** 未返回状态 \_ SUCCESS，则驱动程序将返回，而不进行其他处理。

2.  检查输出参数的有效性。 对于包含有效输出数据的 *outputBuffer* ，必须将 **签名** 设置为 ACPI \_ EVAL \_ 输出 \_ 缓冲区 \_ 签名，并且 **Count** 必须设置为大于零。

3.  处理传回驱动程序的输出参数。

4.  调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 以完成 IOCTL \_ ACPI \_ EVAL \_ 方法请求。

以下示例中使用的 ACPI 数据结构和常量是在 *Acpiioct*中定义的。

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

 

