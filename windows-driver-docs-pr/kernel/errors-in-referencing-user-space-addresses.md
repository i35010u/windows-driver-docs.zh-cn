---
title: 引用用户空间地址时出错
description: 引用用户空间地址时出错
ms.assetid: 87944805-e4ba-431e-b673-b0125dc9ec24
keywords:
- 可靠性 WDK 内核，用户空间地址
- 引用 WDK 内核的用户空间地址
- 引用用户-空间地址
- 嵌入指针 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6bbfb7269f4aab1f97059fc28a15cb86a2aa975
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838706"
---
# <a name="errors-in-referencing-user-space-addresses"></a>引用用户空间地址时出错





任何驱动程序（无论是支持 Irp 还是快速 i/o 操作）都应该验证用户空间中的任何地址，然后再尝试使用它。 I/o 管理器不会验证此类地址，也不会验证已传递给驱动程序的缓冲区中嵌入的指针。

### <a href="" id="failure-to-validate-addresses-passed-in-method-neither-ioctls-and-fsctls"></a>验证传入方法的地址不\_IOCTLs 和 FSCTLs 失败

对于 IOCTLs 和 FSCTLs 方法\_，i/o 管理器不执行任何验证。 为了确保用户空间地址有效，驱动程序必须使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)和[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)例程，并将所有缓冲区引用包含在**try/except**块中。

在下面的示例中，驱动程序假定在**Type3InputBuffer**中传递的值表示有效地址。

```cpp
   case IOCTL_GET_HANDLER:
   {
      PULONG EntryPoint;

      EntryPoint =
         IrpSp->Parameters.DeviceIoControl.Type3InputBuffer; 
      *EntryPoint = (ULONG)DriverEntryPoint; 
      ...
   }
```

以下代码可避免此问题：

```cpp
   case IOCTL_GET_HANDLER:
   {
      PULONG_PTR EntryPoint;

      EntryPoint =
         IrpSp->Parameters.DeviceIoControl.Type3InputBuffer;
 
      try
      {
         if (Irp->RequestorMode != KernelMode)
         { 
            ProbeForWrite(EntryPoint,
                          sizeof(ULONG_PTR),
                          TYPE_ALIGNMENT(ULONG_PTR));
         }
         *EntryPoint = (ULONG_PTR)DriverEntryPoint;
      }
      except(EXCEPTION_EXECUTE_HANDLER)
      {
        ...
      }
      ...
   }
```

另请注意，正确的代码将**DriverEntryPoint**转换为 ULONG\_PTR，而不是 ulong。 此更改允许在64位 Windows 环境中使用。

### <a name="failure-to-validate-pointers-embedded-in-buffered-io-requests"></a>未能验证嵌入在缓冲 i/o 请求中的指针

通常，驱动程序会在缓冲请求中嵌入指针，如以下示例中所示：

```cpp
   struct ret_buf
   {
      void  *arg;  // Pointer embedded in request
      int  rval;
   };

   pBuf = Irp->AssociatedIrp.SystemBuffer;
   ...
   arg = pBuf->arg;  // Fetch the embedded pointer
   ...
   // If the arg pointer is not valid, the following
   // statement can corrupt the system:
   RtlMoveMemory(arg, &info, sizeof(info));
```

在此示例中，驱动程序应使用 IOCTLs 中所述的\_方法，通过使用在**try/except**块中包含的**探测器 * Xxx*** 例程来验证嵌入指针。 尽管嵌入指针允许驱动程序返回额外信息，但驱动程序可以通过使用相对偏移量或可变长度缓冲区来更有效地获得相同的结果。

有关使用**try/except**块处理无效地址的详细信息，请参阅[处理异常](handling-exceptions.md)。

 

 




