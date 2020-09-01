---
title: 无法初始化输出缓冲区
description: 无法初始化输出缓冲区
ms.assetid: 8c038a94-8506-44e3-ac7f-82b58d791124
keywords:
- 输出缓冲区 WDK 内核
- 初始化输出缓冲区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b5069ce9d6e1a0b5d1b67d27fb0a68dbcf178ae
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189063"
---
# <a name="failure-to-initialize-output-buffers"></a>无法初始化输出缓冲区





驱动程序应在将输出缓冲区返回给调用方之前，先将其初始化为零。 如果无法初始化缓冲区，则可能会导致在任何未初始化的字节中产生垃圾数据。

在下面的示例中，驱动程序以未使用的字节返回垃圾。

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

将 **IoStatus** 设置为输出缓冲区大小会导致整个输出缓冲区返回给调用方。 I/o 管理器不会初始化超出输入缓冲区大小的数据—缓冲请求的输入和输出缓冲区重叠。 由于系统支持例程 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 不会写入整个缓冲区，因此此 IOCTL 会将未初始化的数据返回给调用方。

某些驱动程序使用 **信息** 字段返回提供有关 i/o 请求的额外详细信息的代码。 在执行此操作之前，此类驱动程序应检查 IRP 标志，以确保 \_ \_ 未设置 irp 输入操作。 如果未设置此标志，IOCTL 或 FSCTL 没有输出缓冲区，因此 **信息** 字段不需要提供缓冲区大小。 在这种情况下。 驱动程序可以安全地使用 **信息** 字段返回其自己的代码。

 

