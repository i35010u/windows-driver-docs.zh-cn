---
title: 方法 2 使用 IoIs32bitProcess
description: 方法 2 使用 IoIs32bitProcess
ms.assetid: 41e9c0e6-59dd-4e01-9c82-5aba40d8b97f
keywords:
- 32 位 I/O 支持 WDK 64 位 IoIs32bitProcess
- IoIs32bitProcess
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296c8ca40fc530fead46a45c5be8499c62e7d77a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382962"
---
# <a name="technique-2-using-iois32bitprocess"></a>方法 2：使用 IoIs32bitProcess





在其中不定义从 32 位和 64 位应用程序的 I/O 请求的单独 IOCTL 或 FSCTL 控制代码可行的情况下，将由驱动程序来确定哪种类型的应用程序发送的 I/O 请求。 Microsoft Windows 的 64 位版本引入了一个新的内核模式例程[ **IoIs32bitProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iois32bitprocess)，，用于检测当前的 I/O 请求是否源自在 32 位用户模式进程中。 其原型是：

```cpp
BOOLEAN
  IoIs32bitProcess(
    _In_opt_ PIRP Irp  // NULL for fast I/O call, IRP otherwise
    );
```

**IoIs32bitProcess**将返回**TRUE**如果当前的 I/O 请求的发起方是一个 32 位用户模式应用程序。

下面的代码示例演示如何使用**IoIs32bitProcess**:

```cpp
typedef UINT32 POINTER_32 PVOID32;

typedef struct _IOCTL_PARAMETERS
{
    PVOID   Addr;
    SIZE_T  Length;
    HANDLE  Handle;
} IOCTL_PARAMETERS, *PIOCTL_PARAMETERS;

typedef struct _IOCTL_PARAMETERS_32
{
    PVOID32  Addr;
    INT32    Length;
    PVOID32  Handle;
} IOCTL_PARAMETERS_32, *PIOCTL_PARAMETERS_32;

...

IOCTL_PARAMETERS LocalParam;

if (IoIs32bitProcess(Irp))
{ 
    /* 32-bit process IOCTL */
    PIOCTL_PARAMETERS_32 params32;

    params32 = (PIOCTL_PARAMETERS_32)(Irp->AssociatedIrp.SystemBuffer);
    if (irpSp->Parameters.DeviceIoControl.InputBufferLength < sizeof(IOCTL_PARAMETERS_32))
    {
        status = STATUS_INVALID_PARAMETER;
    }
    else
    {
        LocalParam.Addr = Ptr32ToPtr(params32->Addr);
        LocalParam.Handle = Handle32ToHandle(params32->Handle);
        LocalParam.Length = params32->Length;

        /* Handle the IOCTL here. */
        ...

        status = STATUS_SUCCESS;
        Irp->IoStatus.Information = 0;
    }
}
else
{  
    /* 64-bit process IOCTL */
    PIOCTL_PARAMETERS params;

    params = (PIOCTL_PARAMETERS)(Irp->AssociatedIrp.SystemBuffer);
    if (irpSp->Parameters.DeviceIoControl.InputBufferLength < sizeof(IOCTL_PARAMETERS))
    {
        status = STATUS_INVALID_PARAMETER;
    }
    else
    {
        RtlCopyMemory(&LocalParam, params, sizeof(IOCTL_PARAMETERS));

        /* Handle the IOCTL here. */
        ...

        status = STATUS_SUCCESS;
    }
    Irp->IoStatus.Information = 0;
}
```

 

 




