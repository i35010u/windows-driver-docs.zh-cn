---
title: 引用用户空间地址时出错
description: 引用用户空间地址时出错
ms.assetid: 87944805-e4ba-431e-b673-b0125dc9ec24
keywords:
- 可靠性 WDK 内核，用户空间地址
- 引用 WDK 内核的用户空间地址
- 引用用户空间地址
- 嵌入式的指针 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bdf3ea2d23319a461de5a30ce7a9608946a2912
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385130"
---
# <a name="errors-in-referencing-user-space-addresses"></a>引用用户空间地址时出错





任何驱动程序是否支持 Irp 或快速 I/O 操作，应在用户空间中的任何地址前验证尝试使用它。 I/O 管理器不会验证此类地址，也不会验证缓冲区传递给驱动程序中嵌入的指针。

### <a href="" id="failure-to-validate-addresses-passed-in-method-neither-ioctls-and-fsctls"></a>无法验证地址在方法中传递\_NEITHER Ioctl 和 FSCTLs

I/O 管理器会执行任何验证技术方法\_既不 Ioctl 和 FSCTLs。 若要确保用户空间地址都有效，则驱动程序必须使用[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)并[ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)例程，中的所有缓冲区引用都封闭**试用 / 除外**块。

在以下示例中，驱动程序假定中传递的值**Type3InputBuffer**表示有效的地址。

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

下面的代码可避免此问题：

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

另请注意，正确的代码将强制转换**DriverEntryPoint** ULONG 到\_PTR，而不是 ULONG。 此更改允许在 64 位 Windows 环境中使用。

### <a name="failure-to-validate-pointers-embedded-in-buffered-io-requests"></a>验证指针嵌入在缓冲 I/O 请求失败

通常的驱动程序嵌入指针中缓冲请求，如以下示例所示：

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

在此示例中，驱动程序应通过使用验证嵌入式的指针**探测 * Xxx*** 例程括在**尝试 / except**中用于该方法的相同方式阻止\_既不 Ioctl前面所述。 尽管嵌入指针允许驱动程序返回额外信息，但驱动程序可以通过使用相对偏移量或可变长度缓冲区更有效地实现相同的结果。

有关使用详细信息**试用 / 除外**块以处理无效的地址，请参阅[处理异常](handling-exceptions.md)。

 

 




