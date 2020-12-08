---
title: 使用 IoIs32bitProcess 的方法2
description: 使用 IoIs32bitProcess 的方法2
keywords:
- 32位 i/o 支持 WDK 64 位，IoIs32bitProcess
- IoIs32bitProcess
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d05657290a63d3dc38aae1865787827364776acc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788581"
---
# <a name="technique-2-using-iois32bitprocess"></a>方法 2：使用 IoIs32bitProcess





在不可行的情况下，若要为来自32位和64位应用程序的 i/o 请求定义单独的 IOCTL 或 FSCTL 控制代码，则该驱动程序会将其保留给驱动程序，以确定哪种类型的应用程序发送了 i/o 请求。 64位版本的 Microsoft Windows 引入了一个新的内核模式例程 [**IoIs32bitProcess**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iois32bitprocess)，它检测当前 i/o 请求是否源自32位用户模式进程。 其原型为：

```cpp
BOOLEAN
  IoIs32bitProcess(
    _In_opt_ PIRP Irp  // NULL for fast I/O call, IRP otherwise
    );
```

如果当前 i/o 请求的发起方为32位用户模式应用程序，则 **IoIs32bitProcess** 返回 **TRUE** 。

下面的代码示例演示如何使用 **IoIs32bitProcess**：

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

 

