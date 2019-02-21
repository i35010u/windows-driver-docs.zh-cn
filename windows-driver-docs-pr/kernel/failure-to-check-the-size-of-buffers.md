---
title: 未能检查缓冲区的大小
description: 未能检查缓冲区的大小
ms.assetid: e9d9a5d9-19a5-4a1d-95f9-df2021c51c41
keywords:
- 缓冲区大小 WDK 内核
- 输入的缓冲区 WDK 内核
- 输出缓冲区 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2673d535c8b2d123e5fa6c53f8c9eaeac8583a2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519779"
---
# <a name="failure-to-check-the-size-of-buffers"></a>未能检查缓冲区的大小





在处理 Ioctl 和 FSCTLs 实现缓冲的 I/O 时，驱动程序应始终检查以确保缓冲区可以容纳所有请求的数据的输入和输出缓冲区的大小。 如果该请求指定了文件\_ANY\_访问，因为大多数驱动程序 Ioctl 和 FSCTLs 那样，任何有到设备的句柄的调用方有权访问该设备，缓冲 IOCTL 或 FSCTL 请求和无法读取或写入数据的末尾之外缓冲区。

### <a name="input-buffer-size"></a>输入的缓冲区大小

例如，假定以下代码显示在从调用的例程*调度*例程和驱动程序尚未验证 IRP 中传递的缓冲区大小：

```cpp
   switch (ControlCode)
      ...
      ...
      case IOCTL_NEW_ADDRESS:{
         tNEW_ADDRESS *pNewAddress = 
            pIrp->AssociatedIrp.SystemBuffer;

         pDeviceContext->Addr = RtlUlongByteSwap (pNewAddress->Address);
```

该示例不会检查 （突出显示） 的赋值语句前的缓冲区大小。 因此， **pNewAddress-&gt;地址**中的下一步的行的引用可以容错，如果输入的缓冲区不够大，无法包含 tNEW\_地址结构。

下面的代码检查缓冲区大小，从而避免潜在的问题：

```cpp
   case IOCTL_NEW_ADDRESS: {
      tNEW_ADDRESS *pNewAddress =
         pIrp->AssociatedIrp.SystemBuffer;

      if (pIrpSp->Parameters.DeviceIoControl.InputBufferLength >=
             sizeof(tNEW_ADDRESS)) {
         pDeviceContext->Addr = RtlUlongByteSwap (pNewAddress->Address);
```

代码以处理其他缓冲的 I/O，例如使用可变大小的缓冲区的 WMI 请求可以具有类似的错误。

### <a name="output-buffer-size"></a>输出缓冲区大小

输出缓冲区问题都是类似于输入缓冲区问题。 它们可以轻松地损坏池，并且用户模式下调用方可能并不知道已发生的任何错误。

在以下示例中，该驱动程序无法签入的大小**SystemBuffer**:

```cpp
   case IOCTL_GET_INFO: {

       Info = Irp->AssociatedIrp.SystemBuffer;

       Info->NumIF = NumIF;
       ...
       ...
       Irp->IoStatus.Information =
             NumIF*sizeof(GET_INFO_ITEM)+sizeof(ULONG);
       Irp->IoStatus.Status = ntStatus;
   }
```

假设**NumIF**系统缓冲区的字段指定的输入项的数目，此示例中可以设置**IoStatus.Information**到的值大于输出缓冲区，因此返回过多对用户模式代码的信息。 如果未正确编码应用程序，并使用太小的输出缓冲区，前面的代码中调用可能会损坏该池由系统缓冲区的末尾之外写入。

请记住 I/O 管理器假定中的值**信息**字段才有效。 如果调用方通过有效的内核模式地址中的输出缓冲区和大小的零字节，如果该驱动程序不检查输出缓冲区大小，从而找出错误可能发生严重问题。

 

 




