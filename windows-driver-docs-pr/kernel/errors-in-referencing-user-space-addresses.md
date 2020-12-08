---
title: 引用用户空间地址时出错
description: 引用用户空间地址时出错
keywords:
- 可靠性 WDK 内核，用户空间地址
- 引用 WDK 内核的用户空间地址
- 引用用户-空间地址
- 嵌入指针 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99e081913239f2aa1edc162f38bbe76d95b6576a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838773"
---
# <a name="errors-in-referencing-user-space-addresses"></a>引用用户空间地址时出错





任何驱动程序（无论是支持 Irp 还是快速 i/o 操作）都应该验证用户空间中的任何地址，然后再尝试使用它。 I/o 管理器不会验证此类地址，也不会验证已传递给驱动程序的缓冲区中嵌入的指针。

### <a name="failure-to-validate-addresses-passed-in-method_neither-ioctls-and-fsctls"></a><a href="" id="failure-to-validate-addresses-passed-in-method-neither-ioctls-and-fsctls"></a>未能验证传入方法的地址 \_ 不是 IOCTLs 和 FSCTLs

对于 IOCTLs 和 FSCTLs 方法，i/o 管理器不执行任何验证 \_ 。 为了确保用户空间地址有效，驱动程序必须使用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread) 和 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite) 例程，并将所有缓冲区引用包含在 **try/except** 块中。

在下面的示例中，驱动程序假定在 **Type3InputBuffer** 中传递的值表示有效地址。

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

另请注意，正确的代码将 **DriverEntryPoint** 转换为 ulong \_ PTR，而不是 ulong。 此更改允许在64位 Windows 环境中使用。

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

在此示例中，驱动程序应通过使用在 **try/except** 块中包含的 **探测器 * Xxx*** 例程来验证嵌入的指针，方法与前面介绍的方法均不是 IOCTLs 的方法相同 \_ 。 尽管嵌入指针允许驱动程序返回额外信息，但驱动程序可以通过使用相对偏移量或可变长度缓冲区来更有效地获得相同的结果。

有关使用 **try/except** 块处理无效地址的详细信息，请参阅 [处理异常](handling-exceptions.md)。

 

