---
title: 无法初始化输出缓冲区
description: 无法初始化输出缓冲区
ms.assetid: 8c038a94-8506-44e3-ac7f-82b58d791124
keywords:
- 输出缓冲区 WDK 内核
- 初始化输出缓冲区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94dcc2403f1d6ec633a20f9fd23dcbd874efb489
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359999"
---
# <a name="failure-to-initialize-output-buffers"></a>无法初始化输出缓冲区





驱动程序应初始化用零之前将其返回给调用方的所有输出缓冲区。 无法初始化缓冲区可能会导致垃圾回收中未初始化的任何字节的数据。

在以下示例中，驱动程序返回垃圾回收中未使用的字节数。

```cpp
   case IOCTL_GET_NAME: {
      ...
      ...
      outputBufferLength = 
         ioStack->Parameters.DeviceIoControl.OutputBufferLength;
      outputBuffer = (PGET_NAME) Irp->AssociatedIrp.SystemBuffer;
 
      if (outputBufferLength >= sizeof(GET_NAME)) {
         length = outputBufferLength - sizeof(GET_NAME);
 
         ntStatus = IoGetDeviceProperty(
                        DeviceExtension->PhysicalDeviceObject,
                        DevicePropertyDriverKeyName,
                        length,
                        outputBuffer->DriverKeyName,
                        &length);

         outputBuffer->ActualLength =
                        length + sizeof(GET_NAME);

         Irp->IoStatus.Information = outputBufferLength;
 
      } else {
         ntStatus = STATUS_BUFFER_TOO_SMALL;
      }
```

设置**IoStatus.Information**为输出缓冲区大小会导致整个输出缓冲区返回给调用方。 I/O 管理器不会初始化超出输入缓冲区的大小的数据-为缓冲请求重叠的输入和输出缓冲区。 由于系统支持例程[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)不会写入整个缓冲区中，此 IOCTL 返回给调用方未初始化的数据。

某些驱动程序使用**信息**字段返回提供有关输入/输出请求的额外详细信息的代码。 这样做之前，此类驱动程序应检查 IRP 标志，以确保该 IRP\_输入\_未设置操作。 如果未设置此标志，IOCTL 或 FSCTL 不具有输出缓冲区，因此**信息**字段不需要提供的缓冲区大小。 在这种情况下。 可以安全地使用该驱动程序**信息**字段要返回其自己的代码。

 

 




