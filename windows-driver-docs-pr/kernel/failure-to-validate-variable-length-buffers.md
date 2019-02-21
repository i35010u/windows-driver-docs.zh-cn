---
title: 未能验证长度可变的缓冲区
description: 未能验证长度可变的缓冲区
ms.assetid: 0cc4be22-8197-421a-a5a6-2e7b89a79a38
keywords:
- 输入的缓冲区 WDK 内核
- 长度可变的输入的缓冲区 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: be723319ea8d6b2419f40e83068f0e6d0e6f0bb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533811"
---
# <a name="failure-to-validate-variable-length-buffers"></a>未能验证长度可变的缓冲区





驱动程序通常接受输入的缓冲区的固定标头和尾部可变长度数据，如以下示例所示：

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

如果**WaitBuffer-&gt;NameLength**是一个非常大的 ULONG 值，将添加到偏移量，可能会导致整数溢出。 相反，驱动程序应该减去的偏移**InputBufferLength**，并将结果与进行比较**WaitBuffer-&gt;NameLength**，如以下示例：

```cpp
   if (InputBufferLength < sizeof(WAIT_FOR_BUFFER)) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      Return( STATUS_INVALID_PARAMETER );
   }

   WaitBuffer = Irp->AssociatedIrp.SystemBuffer;

   if ((InputBufferLength -
         FIELD_OFFSET(WAIT_FOR_BUFFER, Name[0])  >
         WaitBuffer->NameLength) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      return( STATUS_INVALID_PARAMETER );
   }
```

上述减法无法下溢，因为第一个**如果**语句可确保**InputBufferLength**大于或等于的大小**等待\_为\_缓冲区**。

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

在此示例中，在乘法会发生整数溢出。 如果的大小**设置\_值\_信息**结构是 2 的倍数**NumEntries**值如 0x80000000 导致溢出时，bits 时期间的左移乘法。 但是，缓冲区大小将不过通过验证测试，因为溢出会导致**dwSize**才会显示相当小。 若要避免此问题，如前面的示例中所示的长度减去、 除以**sizeof**(**设置\_值\_信息**)，并比较结果与**NumEntries**。

 

 




