---
title: 无法验证长度可变的缓冲区
description: 无法验证长度可变的缓冲区
keywords:
- 输入缓冲 WDK 内核
- 可变长度输入缓冲 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 990d5055ac8c42eeb40fdca8c104c5fea310eac7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832299"
---
# <a name="failure-to-validate-variable-length-buffers"></a>无法验证长度可变的缓冲区





驱动程序通常接受带有固定标头和尾随可变长度数据的输入缓冲区，如以下示例中所示：

```cpp
   typedef struct _WAIT_FOR_BUFFER {
      LARGE_INTEGER Timeout;
      ULONG NameLength;
      BOOLEAN TimeoutSpecified;
      WCHAR Name[1];
   } WAIT_FOR_BUFFER, *PWAIT_FOR_BUFFER;

   if (InputBufferLength < sizeof(WAIT_FOR_BUFFER)) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      return( STATUS_INVALID_PARAMETER );
   }

   WaitBuffer = Irp->AssociatedIrp.SystemBuffer;

   if (FIELD_OFFSET(WAIT_FOR_BUFFER, Name[0]) +
          WaitBuffer->NameLength > InputBufferLength) {
       IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
       return( STATUS_INVALID_PARAMETER );
   }
```

如果 **WaitBuffer- &gt; NameLength** 是非常大的 ULONG 值，则将其添加到偏移量可能导致整数溢出。 相反，驱动程序应将偏移量 (固定标头大小) 从 **InputBufferLength** (缓冲区大小) 中减去，并测试结果是否为 **WaitBuffer- &gt; NameLength** (可变长度数据) 留出足够的空间，如以下示例中所示：

```cpp
   if (InputBufferLength < sizeof(WAIT_FOR_BUFFER)) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      Return( STATUS_INVALID_PARAMETER );
   }

   WaitBuffer = Irp->AssociatedIrp.SystemBuffer;

   if ((InputBufferLength -
         FIELD_OFFSET(WAIT_FOR_BUFFER, Name[0])  <
         WaitBuffer->NameLength) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      return( STATUS_INVALID_PARAMETER );
   }
```

换而言之，如果缓冲区大小减去固定标头大小的长度少于可变长度数据所需的字节数，则返回失败。

上述减法不能下溢，因为第一个 **if** 语句可确保 **InputBufferLength** 大于或等于 **等待 \_ \_ 缓冲区** 的大小。

下面显示了更复杂的溢出问题：

```cpp
   case IOCTL_SET_VALUE:
      dwSize = sizeof(SET_VALUE);

      if (inputBufferLength < dwSize) {
         ntStatus = STATUS_BUFFER_TOO_SMALL;
         break;
      }

      dwSize = FIELD_OFFSET(SET_VALUE, pInfo[0]) +
                  pSetValue->NumEntries * sizeof(SET_VALUE_INFO);

      if (inputBufferLength < dwSize) {
         ntStatus = STATUS_BUFFER_TOO_SMALL;
         break;
      }
```

在此示例中，在乘法运算期间可能发生整数溢出。 如果 **集 \_ 值 \_ 信息** 结构的大小是2的倍数，则当在乘法运算期间将位向左移位时， **NumEntries** 值（例如0x80000000）会导致溢出。 但是，缓冲区大小仍将通过验证测试，因为溢出会导致 **dwSize** 显示得相当小。 若要避免此问题，请将上一示例中的长度减去（除以 **sizeof** (**设置 \_ 值 \_ 信息**) ），并将结果与 **NumEntries** 进行比较。

 

 




