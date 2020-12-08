---
title: 发送 IOCTL_ACPI_ENUM_CHILDREN 请求
description: 发送 IOCTL_ACPI_ENUM_CHILDREN 请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4026c9fab1cc389ae64db86e7b23dbd99063f6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789469"
---
# <a name="sending-an-ioctl_acpi_enum_children-request"></a>发送 IOCTL \_ ACPI \_ 枚举 \_ 子请求


驱动程序通常使用两个 [**IOCTL \_ ACPI \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_enum_children) 请求的序列来枚举要向其发送请求的设备的命名空间中感兴趣的对象。 驱动程序将发送第一个请求，以获取包含对象的路径和名称所需的驱动程序分配输出缓冲区的大小。 驱动程序发送第二个请求以返回驱动程序分配的输出缓冲区中的对象的路径和名称。

下面的代码示例演示如何发送两个同步 IOCTL \_ ACPI \_ 枚举子请求的序列， \_ 以递归枚举将请求发送到的父设备的所有子设备。 此代码执行以下操作序列来处理第一个请求：

1.  为第一个请求设置输入缓冲区。 输入缓冲区是一个 [**ACPI \_ 枚举 \_ 子 \_ 输入 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_input_buffer) 结构，其 **签名** 设置为枚举 \_ 子级 \_ 输入 \_ 缓冲区 \_ 签名， **标志** 设置为枚举 \_ 子级 \_ 多级。

2.  设置第一个请求的输出缓冲区。 输出缓冲区设置为 [**ACPI \_ 枚举 \_ 子 \_ 输出 \_ 缓冲区**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_children_output_buffer) 结构。 此输出缓冲区只包含一个 [**ACPI \_ 枚举 \_ 子**](/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_enum_child) 结构，此结构的大小不足以返回设备的名称。

3.  调用调用方提供的 [SendDownStreamIrp 函数](senddownstreamirp-function.md) ，以同步方式将第一个请求发送到父设备。

4.  检查 ACPI 驱动程序是否将返回状态设置为状态 \_ 缓冲区 \_ 溢出。 如果返回了其他状态，则表明出现了错误，代码已终止。

5.  检查 ACPI 驱动程序是否将 **签名** 成员设置为 ACPI \_ 枚举 \_ 子 \_ 输出 \_ 缓冲区 \_ 签名，并将 **NUMBEROFCHILDREN** 设置为大于或等于 **sizeof** (ACPI \_ 枚举 \_ 子 \_ 输出 \_ 缓冲区) 的值。 如果两者都为 true，则 **NumberOfChildren** 的值是输出缓冲区的大小（以字节为单位），它需要包含请求的子对象名称。

示例代码获取所需的输出缓冲区大小后，它将执行以下操作序列来处理第二个请求，该请求将返回所请求子对象的路径和名称：

1.  分配所需大小的输出缓冲区（以字节为单位）。

2.  调用驱动程序提供的 **SendDownStreamIrp** 函数，以同步方式向父设备发送第二个请求。

3.  检查 ACPI 驱动程序是否将 **签名** 成员设置为 ACPI \_ 枚举 \_ 子 \_ 输出 \_ 缓冲区 \_ 签名，将 **NumberOfChildren** 设置为一个或多个 (，以指示已) 至少返回一个对象的路径和名称，并将 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)的 **信息** 成员设置为输出缓冲区的已分配大小。

4.  在输出缓冲区中处理子对象名称的数组。

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

 

