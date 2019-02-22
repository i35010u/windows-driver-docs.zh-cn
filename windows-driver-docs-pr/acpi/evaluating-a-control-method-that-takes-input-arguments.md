---
title: 评估采用输入的参数的控制方法
description: 评估采用输入的参数的控制方法
ms.assetid: 3a4be8a8-0906-4d38-bf6d-f245e6ae236a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cad6bc7b279af08b276a0e90c1fd8e2fecf0248
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542000"
---
# <a name="evaluating-a-control-method-that-takes-input-arguments"></a>评估采用输入的参数的控制方法


若要以同步方式评估采用输入的参数的控制方法，设备的驱动程序发送[ **IOCTL\_ACPI\_EVAL\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff536148)请求或[**IOCTL\_ACPI\_EVAL\_方法\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff536149)到设备的请求。 使用这两个这些请求的一般过程所述[评估 ACPI 控件方法以同步方式](evaluating-acpi-control-methods-synchronously.md)。 使用以下两个请求的特定区别是，如下所示：

-   如果控件方法在设备的直接子对象，该驱动程序将发送 IOCTL\_ACPI\_EVAL\_方法请求并提供一个为以下输入结构：[**ACPI\_EVAL\_输入\_缓冲区\_简单\_整数**](https://msdn.microsoft.com/library/windows/hardware/ff536119)， [ **ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串**](https://msdn.microsoft.com/library/windows/hardware/ff536121)，或[ **ACPI\_EVAL\_输入\_缓冲区\_复杂**](https://msdn.microsoft.com/library/windows/hardware/ff536116).

-   如果控件方法是在设备的 ACPI 命名空间中的子对象，但不是设备的直接子对象，该驱动程序将发送 IOCTL\_ACPI\_EVAL\_方法\_EX 请求并提供一个的以下输入的结构：[**ACPI\_EVAL\_输入\_缓冲区\_简单\_整数\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536120)， [ **ACPI\_EVAL\_输入\_缓冲区\_简单\_字符串\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536122)，或者[ **ACPI\_EVAL\_输入\_缓冲区\_复杂\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff536117)。

该示例*EvaluateABCDWithInputArgument*本主题中提供的函数显示如何将驱动程序可以使用 IOCTL\_ACPI\_EVAL\_评估名为的控制方法的方法请求ABCD 采用单个整数输入的参数。

如果输入的参数是字符串或自定义数据而不是整数的数组，对示例代码所需的更改是提供字符串输入的结构或复杂的输入的结构，而不是整数输入结构。

此外，如果 ABCD 控件方法不是直接子对象，对示例代码所需的更改如下所示：

-   发送 IOCTL\_ACPI\_EVAL\_方法\_EX 请求而不是 IOCTL\_ACPI\_EVAL\_方法请求。

-   提供了扩展 （简单的整数、 简单的字符串或复杂） 的输入的参数类型相对应的输入结构的类型。

*EvaluateABCDWithInputArgument*首先会分配 ACPI\_EVAL\_输入\_缓冲区\_简单\_整数结构*inputBuffer* ，然后设置**MethodNameAsUlong**成员的名称是控制方法，设置**IntegerArgument**成员添加到输入的整数值和集**签名**成员添加到 ACPI\_EVAL\_输入\_缓冲区\_简单\_整数\_签名。

```cpp
    // Fill in the input data
    inputBuffer.MethodNameAsUlong = (ULONG) ('DCBA');
    inputBuffer.IntegerArgument  =  Argument1;
    inputBuffer.Signature = ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_SIGNATURE;
```

*EvaluateABCDWithInputArgument*还会分配[ **ACPI\_EVAL\_输出\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff536123)结构*outputBuffer*，但未设置任何的成员*outputBuffer*。

*EvaluateABCDWithInputArgument*然后调用一个名为驱动程序提供函数[SendDownStreamIrp](senddownstreamirp-function.md) ，执行以下：

1.  调用[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)要生成请求。

2.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)发送关闭设备堆栈请求。

3.  等待 I/O 管理器，以指示驱动程序的较低级驱动程序已完成请求。

**SendDownStreamIrp** I/O 管理器发出信号的较低级驱动程序已完成请求后返回。

尽管未包含在*EvaluateABCDWithInputArgument*，该驱动程序还应执行以下附加操作后的**SendDownStreamIrp**返回：

1.  检查状态， **SendDownStreamIrp**返回。 如果**SendDownStreamIrp**不会返回状态\_成功，则驱动程序应返回而无需其他处理。

2.  检查输出参数的有效性。 有关*outputBuffer*包含有效的输出数据**签名**必须设置为 ACPI\_EVAL\_输出\_缓冲区\_签名和**计数**必须设置为大于零。

3.  处理传递到驱动程序的输出参数。

4.  调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完成 IOCTL\_ACPI\_EVAL\_方法请求。

中定义的 ACPI 数据结构和在下面的示例使用常量*Acpiioct.h*。

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

 

 




