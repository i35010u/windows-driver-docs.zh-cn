---
title: 发送 IOCTL_ACPI_ENUM_CHILDREN 请求
description: 发送 IOCTL_ACPI_ENUM_CHILDREN 请求
ms.assetid: cbad53dd-4320-4920-9d16-231d0aaae839
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 620b75352436551925c185984b6c5ed24fcf1ef0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522431"
---
# <a name="sending-an-ioctlacpienumchildren-request"></a>发送 IOCTL\_ACPI\_枚举\_子级请求


驱动程序通常使用两个序列[ **IOCTL\_ACPI\_枚举\_子级**](https://msdn.microsoft.com/library/windows/hardware/ff536147)枚举到设备的命名空间中的相关对象的请求将它发送请求。 该驱动程序将发送第一个请求来获取包含的路径和名称的对象的所需的驱动程序分配输出缓冲区的大小。 该驱动程序将发送第二个请求，以便在驱动程序分配输出缓冲区中返回的路径和名称的对象。

以下代码示例演示如何将发送一系列两个同步 IOCTL\_ACPI\_枚举\_子级请求以递归方式枚举父设备将请求发送的所有子设备。 该代码执行以下一系列操作以处理第一个请求：

1.  设置第一个请求的输入的缓冲区。 输入的缓冲区[ **ACPI\_ENUM\_子级\_输入\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff536110)结构**签名**设置枚举\_子级\_输入\_缓冲区\_签名并**标志**设置为枚举\_子级\_MULTILEVEL。

2.  设置第一个请求的输出缓冲区。 输出缓冲区设置为[ **ACPI\_ENUM\_子级\_输出\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff536112)结构。 此输出缓冲区只包含一个[ **ACPI\_ENUM\_子**](https://msdn.microsoft.com/library/windows/hardware/ff536109)结构，这是不足够大，以返回设备的名称。

3.  调用调用方提供[SendDownStreamIrp 函数](senddownstreamirp-function.md)将以同步方式将第一个请求发送到父设备。

4.  检查是否 ACPI 驱动程序将返回状态设置为状态\_缓冲区\_溢出。 如果返回另一个状态，则表明发生了错误，代码将终止。

5.  ACPI 驱动程序设置的检查**签名**成员添加到 ACPI\_ENUM\_子级\_输出\_缓冲区\_签名和集**NumberOfChildren**为值大于或等于**sizeof**(ACPI\_枚举\_子级\_输出\_缓冲区)。 如果两者都是 true 的值**NumberOfChildren**是以字节为单位，包含请求的子对象名称所需的输出缓冲区的大小。

此示例代码将获取所需的输出缓冲区大小后，它将执行以下一系列操作来处理返回的路径和名称的请求的子对象的第二个请求：

1.  分配输出缓冲区的所需的大小，以字节为单位。

2.  调用的驱动程序提供**SendDownStreamIrp**函数以同步方式将第二个请求发送到父设备。

3.  ACPI 驱动程序设置的检查**签名**成员添加到 ACPI\_ENUM\_子级\_输出\_缓冲区\_签名，设置**NumberOfChildren**到一个或多个 （指示返回的路径和名称的至少一个对象），并设置**信息**的成员[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)到输出缓冲区的分配大小。

4.  处理的输出缓冲区中的子对象名称的数组。

```cpp
#define MY_TAG 'gTyM'   // Pool tag for memory allocation

 ACPI_ENUM_CHILDREN_INPUT_BUFFER  inputBuffer;
    ACPI_ENUM_CHILDREN_OUTPUT_BUFFER outputSizeBuffer = { 0 };
    ACPI_ENUM_CHILDREN_OUTPUT_BUFFER outputBuffer = { 0 };
    ULONG                            bufferSize;
 PACPI_ENUM_CHILD                 childObject = NULL;
 ULONG                            index;

    NTSTATUS                         status;

    ASSERT( ReturnStatus != NULL );
    *ReturnStatus = 0x0;

    // Fill in the input data
    inputBuffer.Signature = ACPI_ENUM_CHILDREN_INPUT_BUFFER_SIGNATURE;
    inputBuffer.Flags = ENUM_CHILDREN_MULTILEVEL;

    // Send the request along
    status = SendDownStreamIrp(
       Pdo,
 IOCTL_ACPI_ENUM_CHILDREN,
       &inputBuffer,
       sizeof(inputBuffer),
       &outputSizeBuffer,
       sizeof(outputSizeBuffer)
       );

 if (Status != STATUS_BUFFER_OVERFLOW) {
        // There should be at least one child device (that is the device itself)
        // Return error return status
    }

    // Verify the data
    // NOTE: The NumberOfChildren returned by ACPI actually contains the required size
 // when the status returned is STATUS_BUFFER_OVERFLOW 

    if ((outputSizeBuffer.Signature != ACPI_ENUM_CHILDREN_OUTPUT_BUFFER_SIGNATURE) ||
       (outputSizeBuffer.NumberOfChildren < sizeof(ACPI_ENUM_CHILDREN_OUTPUT_BUFFER)))
    {
        return STATUS_ACPI_INVALID_DATA;
    }

    //
    // Allocate a buffer to hold all the child devices
    //
    bufferSize = outputSizeBuffer.NumberOfChildren;
    outputBuffer = (PACPI_ENUM_CHILDREN_OUTPUT_BUFFER)
 ExAllocatePoolWithTag(PagedPool, bufferSize, MY_TAG);

    if (outputBuffer == NULL){
        return STATUS_INSUFFICIENT_RESOURCES;
    }

    RtlZeroMemory(outputBuffer, bufferSize);

    // Allocate a new IRP with the new output buffer
    // Send another request together with the new output buffer
    status = SendDownStreamIrp(
       Pdo,
 IOCTL_ACPI_ENUM_CHILDREN,
       &inputBuffer,
       sizeof(inputBuffer),
       &outputBuffer,
       bufferSize
       );

    // Verify the data
    if ((outputBuffer->Signature != ACPI_ENUM_CHILDREN_OUTPUT_BUFFER_SIGNATURE) ||
        (outputBuffer->NumberOfChildren == 0) ||
        (IoStatusBlock.Information != bufferSize)) {
        return STATUS_ACPI_INVALID_DATA;
    }

    // Skip the first child device because ACPI returns the device itself 
 // as the first child device
    childObject = &(outputBuffer->Children[0]);

    for (index = 1; index < outputBuffer->NumberOfChildren; ++index) {

        // Proceed to the next ACPI child device. 
        childObject = ACPI_ENUM_CHILD_NEXT(childObject);

        //  Process each child device.
 
 
 
    }
```

 

 




