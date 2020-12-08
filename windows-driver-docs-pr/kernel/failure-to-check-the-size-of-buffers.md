---
title: 无法检查缓冲区大小
description: 无法检查缓冲区大小
keywords:
- 缓冲区大小 WDK 内核
- 输入缓冲 WDK 内核
- 输出缓冲区 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e03daebced9ab8fbd3d430dcaa8d6a96b6e1cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793551"
---
# <a name="failure-to-check-the-size-of-buffers"></a>无法检查缓冲区大小





当处理实现缓冲 i/o 的 IOCTLs 和 FSCTLs 时，驱动程序应始终检查输入缓冲区和输出缓冲区的大小，以确保缓冲区可以容纳所有请求的数据。 如果请求指定 \_ \_ 了 "文件任何访问权限"，因为大多数驱动程序 IOCTLs 和 FSCTLs，具有设备的句柄的任何调用方都有权访问该设备的缓冲 IOCTL 或 FSCTL 请求，并可能在缓冲区结尾之外读取或写入数据。

### <a name="input-buffer-size"></a>输入缓冲区大小

例如，假设以下代码出现在从 *调度* 例程调用的例程中，并且驱动程序尚未验证 IRP 中传递的缓冲区大小：

```cpp
   switch (ControlCode)
      ...
      ...
      case IOCTL_NEW_ADDRESS:{
         tNEW_ADDRESS *pNewAddress = 
            pIrp->AssociatedIrp.SystemBuffer;

         pDeviceContext->Addr = RtlUlongByteSwap (pNewAddress->Address);
```

该示例不检查)  (突出显示赋值语句之前的缓冲区大小。 因此，如果输入缓冲区不够大，无法包含 tNEW 地址结构，则下一行中的 **pNewAddress &gt;** 引用可能会出错 \_ 。

下面的代码检查缓冲区大小，以避免潜在的问题：

```cpp
   case IOCTL_NEW_ADDRESS: {
      tNEW_ADDRESS *pNewAddress =
         pIrp->AssociatedIrp.SystemBuffer;

      if (pIrpSp->Parameters.DeviceIoControl.InputBufferLength >=
             sizeof(tNEW_ADDRESS)) {
         pDeviceContext->Addr = RtlUlongByteSwap (pNewAddress->Address);
```

处理其他缓冲 i/o 的代码（如使用可变大小缓冲区的 WMI 请求）可能会发生类似的错误。

### <a name="output-buffer-size"></a>输出缓冲区大小

输出缓冲区问题类似于输入缓冲区问题。 它们可以轻松地损坏池，用户模式调用方可能不知道发生了任何错误。

在下面的示例中，驱动程序无法检查 **SystemBuffer** 的大小：

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

假设系统缓冲区的 **NumIF** 字段指定了输入项的数量，则此示例可以将 **IoStatus** 设置为大于输出缓冲区的值，因此会向用户模式代码返回太多信息。 如果应用程序未正确编码，并且调用的输出缓冲区太小，则前面的代码可能会通过写入系统缓冲区结尾之外来损坏池。

请记住，i/o 管理器假定 **信息** 字段中的值有效。 如果调用方为输出缓冲区传入有效的内核模式地址且大小为零字节，则如果驱动程序不检查输出缓冲区大小并因此发现错误，则会出现严重问题。

 

 




