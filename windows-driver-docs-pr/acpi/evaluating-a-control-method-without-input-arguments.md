---
title: 评估不带输入参数的控制方法
description: 评估不带输入参数的控制方法
ms.assetid: dd989b4d-46db-4fe3-aa7b-8dbfe37057cb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a796fc7cd2713b0fcd4ae8ad3af0ce948b3de8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826302"
---
# <a name="evaluating-a-control-method-without-input-arguments"></a>评估不带输入参数的控制方法


若要同步计算不采用输入参数的控制方法，设备的驱动程序将[ **\_acpi\_eval\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)请求或 Ioctl 发送 IOCTL [ **\_acpi\_eval\_方法\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)请求到设备。 [同步评估 ACPI 控制方法](evaluating-acpi-control-methods-synchronously.md)中介绍了这两个请求的一般过程。 使用这两个请求的具体区别如下：

-   如果控制方法是设备的直接子对象，则驱动程序将\_ACPI\_EVAL\_方法请求发送 IOCTL，并提供[**ACPI\_EVAL\_输入\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)输入结构。

-   如果控制方法是设备 ACPI 命名空间中的子对象，但不是设备的直接子对象，则驱动程序将\_ACPI\_EVAL\_方法发送 IOCTL，\_EX 请求并提供[**ACPI\_EVAL\_输入\_缓冲区\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)结构。

本主题中提供的示例*GetAbcData*函数说明了设备的驱动程序如何使用 IOCTL\_ACPI\_EVAL\_方法请求计算设备支持的名为 "ABCD" 的控制方法。 "ABCD" 控制方法是 ACPI 命名空间中的设备的直接子，不接受输入参数或返回输出参数。

如果 "ABCD" 控制方法不是直接子对象，则此示例代码所需的更改如下所示：

-   将 IOCTL\_ACPI\_EVAL\_方法\_EX 请求，而不是使用 IOCTL\_ACPI\_EVAL\_方法请求。

-   提供 ACPI\_EVAL\_输入\_缓冲区\_EX 结构，而不是 ACPI\_EVAL\_的输入\_缓冲区结构。

*GetAbcData*首先分配一个 ACPI\_EVAL\_输入\_缓冲器 structure *inputBuffer* ，并将**MethodNameAsUlong**成员设置为控制方法的名称，并将**签名**成员设置为 ACPI\_EVAL\_输入\_缓冲器\_签名。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIGNATURE;
```

*GetAbcData*还会将[**ACPI\_EVAL\_输出分配\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)结构*outputBuffer*，但不会设置*outputBuffer*的任何成员。

然后， *GetAbcData*调用驱动程序提供的名为[SendDownStreamIrp](senddownstreamirp-function.md)的函数来执行以下操作：

1.  调用[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)以生成请求。

2.  调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将请求发送到设备堆栈中。

3.  等待 i/o 管理器向驱动程序发出低级驱动程序完成请求的信号。

在 i/o 管理器发出请求后， **SendDownStreamIrp**将返回该请求的信号。 前面提到的代码示例执行以下操作：

1.  检查请求的状态，并在较低级别的驱动程序未返回状态\_SUCCESS 时返回而不进行其他处理。

2.  检查输出参数的有效性。 对于包含有效输出数据的*outputBuffer* ，必须将**签名**设置为 ACPI\_EVAL\_输出\_缓冲区\_签名，**计数**必须设置为大于零。

3.  处理 ACPI 驱动程序传递回驱动程序的输出参数。

虽然此步骤未包含在示例代码中，但驱动程序还应在处理输出数据后调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) ，以便\_ACPI\_EVAL\_方法请求或 IOCTL\_acpi 来完成挂起的 IOCTL\_EVAL\_方法请求，驱动程序发送该请求来计算控制方法。

以下示例中使用的 ACPI 数据结构和常量是在*Acpiioct*中定义的。

```cpp
NTSTATUS
GetAbcdData(
    IN PDEVICE_OBJECT   Pdo,
    OUT PULONG          ReturnStatus
    )
/*++

Routine Description:
    Evaluates the ABCD method on the device in the ACPI namespace referenced by Pdo

Parameters
    Pdo             - PDO for the device
    ReturnStatus    - Pointer to where the status data is placed

Return Value:
    NT Status of the operation

--*/
{
    ACPI_EVAL_INPUT_BUFFER  inputBuffer;
    ACPI_EVAL_OUTPUT_BUFFER outputBuffer;
    NTSTATUS                status;
    PACPI_METHOD_ARGUMENT   argument;

    .
    .

    ASSERT( ReturnStatus != NULL );
    *ReturnStatus = 0x0;

    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIGNATURE;

    // Send the request along
    status = SendDownStreamIrp(
       Pdo,
       IOCTL_ACPI_EVAL_METHOD,
       &inputBuffer,
       sizeof(ACPI_EVAL_INPUT_BUFFER),
       &outputBuffer,
       sizeof(ACPI_EVAL_OUTPUT_BUFFER)
       );

    if (!NT_SUCCESS(status)) {
       return status;
    }

    // Verify the data
    if (outputBuffer != NULL) {
        if ( ( (PACPI_EVAL_OUTPUT_BUFFER) outputBuffer->Signature != 
            ACPI_EVAL_OUTPUT_BUFFER_SIGNATURE ||
            ( (PACPI_EVAL_OUTPUT_BUFFER) outputBuffer->Count == 0) {
            return STATUS_ACPI_INVALID_DATA;
        } 
}

    // Retrieve the output argument
    argument = outputBuffer.Argument;
 
// Process the output argument
 .
.
.
 
    return status;
}
```

 

 




