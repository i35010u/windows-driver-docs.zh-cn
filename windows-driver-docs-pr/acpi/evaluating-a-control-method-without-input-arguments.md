---
title: 评估没有输入参数的控制方法
description: 评估没有输入参数的控制方法
ms.assetid: dd989b4d-46db-4fe3-aa7b-8dbfe37057cb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 334fa6bab425915bb4aaeec4721f2450e63c2b96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520733"
---
# <a name="evaluating-a-control-method-without-input-arguments"></a>评估没有输入参数的控制方法


若要以同步方式评估则不使用输入的参数的控制方法，设备的驱动程序发送[ **IOCTL\_ACPI\_EVAL\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff536148)请求或[ **IOCTL\_ACPI\_EVAL\_方法\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff536149)到设备的请求。 使用这两个这些请求的一般过程所述[评估 ACPI 控件方法以同步方式](evaluating-acpi-control-methods-synchronously.md)。 使用以下两个请求的特定区别是，如下所示：

-   如果控件方法在设备的直接子对象，该驱动程序将发送 IOCTL\_ACPI\_EVAL\_方法请求和耗材[ **ACPI\_EVAL\_输入\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff536115)输入结构。

-   如果控件方法是在设备的 ACPI 命名空间中的子对象，但不是设备的直接子对象，该驱动程序将发送 IOCTL\_ACPI\_EVAL\_方法\_EX 请求并提供[**ACPI\_EVAL\_输入\_缓冲区\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff536118)结构。

该示例*GetAbcData*本主题中提供的函数显示设备的驱动程序如何使用 IOCTL\_ACPI\_EVAL\_方法请求用于评估控制方法名为 ABCD 的设备支持。 ABCD 控件方法是在 ACPI 名称空间中的设备的直接子，并且不会采用输入的参数或返回输出参数。

如果 ABCD 控件方法不是直接子对象，此示例代码所需的更改如下所示：

-   发送 IOCTL\_ACPI\_EVAL\_方法\_EX 请求而不是 IOCTL\_ACPI\_EVAL\_方法请求。

-   提供 ACPI\_EVAL\_输入\_缓冲区\_EX 结构而不是 ACPI\_EVAL\_输入\_缓冲区结构。

*GetAbcData*首先会分配 ACPI\_EVAL\_输入\_缓冲区结构*inputBuffer* ，并设置**MethodNameAsUlong**成员添加到控制方法和集名称**签名**成员添加到 ACPI\_EVAL\_输入\_缓冲区\_签名。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIGNATURE;
```

*GetAbcData*还会分配[ **ACPI\_EVAL\_输出\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff536123)结构*outputBuffer*，但未设置任何的成员*outputBuffer*。

*GetAbcData*然后调用一个名为驱动程序提供函数[SendDownStreamIrp](senddownstreamirp-function.md) ，执行以下：

1.  调用[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)要生成请求。

2.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)发送关闭设备堆栈请求。

3.  等待 I/O 管理器，以指示驱动程序的较低级驱动程序已完成请求。

**SendDownStreamIrp** I/O 管理器发出信号的较低级驱动程序已完成请求后返回。 前面所述的代码示例然后执行下列任务：

1.  检查请求的状态，并返回，而不附加处理，如果较低级驱动程序未返回状态\_成功。

2.  检查输出自变量的有效性。 有关*outputBuffer*包含有效的输出数据**签名**必须设置为 ACPI\_EVAL\_输出\_缓冲区\_签名和**计数**必须设置为大于零。

3.  处理输出参数的 ACPI 驱动程序传递回驱动程序。

尽管此步骤中未包含在示例代码，该驱动程序还应调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)之后处理输出数据，以完成挂起 IOCTL\_ACPI\_EVAL\_方法请求或 IOCTL\_ACPI\_EVAL\_方法请求驱动程序发送用于评估控制方法。

中定义的 ACPI 数据结构和在下面的示例使用常量*Acpiioct.h*。

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

 

 




