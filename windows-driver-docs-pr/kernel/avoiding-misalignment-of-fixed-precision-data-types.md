---
title: 避免固定精度数据类型不对齐
description: 避免固定精度数据类型不对齐
ms.assetid: 4e214bd8-b622-447a-b484-bd1d5d239de7
keywords:
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- 控制代码 WDK 64 位
- I/o 控制代码 WDK 内核，64位驱动程序中的32位 i/o
- IOCTLs WDK 内核，64位驱动程序中的32位 i/o
- 指针精度 WDK 64 位
- 固定精度数据类型 WDK 64 位
- 固定精度数据类型未对齐
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5ee7c4b65f72276fe977af236444ba310427c4c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185295"
---
# <a name="avoiding-misalignment-of-fixed-precision-data-types"></a>避免固定精度数据类型不对齐





遗憾的是，对于32位和64位编程，数据类型可能具有相同大小但不同的对齐要求。 因此，将指针精度数据类型更改为固定精度类型不能避免所有的 IOCTL/FSCTL 缓冲区不一致问题。 这意味着，传递包含某些固定精度数据类型的缓冲区的内核模式驱动程序 IOCTLs 和 FSCTLs (或指向它们的指针) 可能也需要 thunked。

### <a name="which-data-types-are-affected"></a>受影响的数据类型

此问题会影响自身结构的固定精度数据类型。 这是因为确定结构的对齐要求的规则是特定于平台的。

例如， ** \_ \_ int64**、大 \_ 整数和 KFLOATING \_ 保存必须在 x86 平台上的4字节边界上对齐。 但在基于 Itanium 的计算机上，它们必须在8字节边界上对齐。

若要确定特定平台上给定数据类型的对齐要求，请使用该平台上的 **类型 \_ 对齐方式** 宏。

### <a name="how-to-fix-the-problem"></a>如何解决此问题

在下面的示例中，IOCTL 是两种 \_ ioctl 都不是的，因此，将 ** &gt; UserBuffer** 指针从用户模式应用程序直接传递到内核模式驱动程序。 对于 IOCTLs 和 FSCTLs 中使用的缓冲区不执行任何验证。 因此，必须先调用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread) 或 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite) ，然后才能安全地取消引用缓冲区指针。

假设32位应用程序已为 **Irp &gt; UserBuffer**传递了有效值，则 \_ 由 **p- &gt; DeviceTime** 指向的大整数结构将按4个字节的边界对齐。 **ProbeForRead** 对照 *传递参数中* 传递的值（在本例中为)  (大整数的 **类型 \_ 对齐** 来检查此对齐方式 \_ 。 在 x86 平台上，此宏表达式返回4个 (字节) 。 但在基于 Itanium 的计算机上，它返回8，导致 **ProbeForRead** 引发状态 \_ 数据类型不 \_ 一致异常。

**注意**   删除**ProbeForRead**调用并不能解决问题，但仅会使诊断变得更困难。

 

```cpp
typedef struct _IOCTL_PARAMETERS2 {
    LARGE_INTEGER DeviceTime;
} IOCTL_PARAMETERS2, *PIOCTL_PARAMETERS2;

#define SETTIME_FUNCTION 1
#define IOCTL_SETTIME CTL_CODE(FILE_DEVICE_UNKNOWN, \
            SETTIME_FUNCTION, METHOD_NEITHER, FILE_ANY_ACCESS)

...

case IOCTL_SETTIME:
    PIOCTL_PARAMETERS2 p = (PIOCTL_PARAMETERS2)Irp->UserBuffer;

    try {                 
        if (Irp->RequestorMode != KernelMode) { 
            ProbeForRead ( p->DeviceTime,
                      sizeof( LARGE_INTEGER ),
                      TYPE_ALIGNMENT( LARGE_INTEGER ));
    }
    status = DoSomeWork(p->DeviceTime);

 } except( EXCEPTION_EXECUTE_HANDLER ) {
```

以下部分介绍如何解决上述问题。 请注意，为了简洁起见，已经编辑了所有代码片段。

### <a name="solution-1-copy-the-buffer"></a>解决方案1：复制缓冲区

若要避免出现不一致问题，最安全的方法是在访问其内容之前创建缓冲区的副本，如以下示例中所示。

```cpp
case IOCTL_SETTIME: {
    PIOCTL_PARAMETERS2 p = (PIOCTL_PARAMETERS2)Irp->UserBuffer;
#if _WIN64
    IOCTL_PARAMETERS2 LocalParams2;

    RtlCopyMemory(&LocalParams2, p, sizeof(IOCTL_PARAMETERS2));
    p = &LocalParams2;
#endif

    status = DoSomeWork(p->DeviceTime);
    break;
}
```

通过首先检查缓冲区内容是否正确对齐，可以优化此解决方案以获得更好的性能。 如果是这样，则可以按原样使用缓冲区。 否则，驱动程序会生成缓冲区的副本。

```cpp
case IOCTL_SETTIME: {
    PIOCTL_PARAMETERS2 p = (PIOCTL_PARAMETERS2)Irp->UserBuffer;
#if _WIN64
    IOCTL_PARAMETERS2 LocalParams2;

    if ( (ULONG_PTR)p & (TYPE_ALIGNMENT(IOCTL_PARAMETERS2)-1)) {
        // The buffer contents are not correctly aligned for this 
        // platform, so copy them into a properly aligned local 
        // buffer.
        RtlCopyMemory(&LocalParams2, p, sizeof(IOCTL_PARAMETERS2));
        p = &LocalParams2;
    }
#endif

    status = DoSomeWork(p->DeviceTime);
    break;
}
```

### <a name="solution-2-use-the-unaligned-macro"></a>解决方案2：使用未对齐的宏

未 **对齐** 的宏告诉 C 编译器生成可访问 **DeviceTime** 字段的代码，而不会发生对齐错误。 请注意，在基于 Itanium 的平台上使用此宏可能会提高驱动程序的大小和速度。

```cpp
typedef struct _IOCTL_PARAMETERS2 {
    LARGE_INTEGER DeviceTime;
} IOCTL_PARAMETERS2;
typedef IOCTL_PARAMETERS2 UNALIGNED *PIOCTL_PARAMETERS2;
```

### <a name="pointers-are-also-affected"></a>指针也会受到影响

前面所述的不一致问题也可能出现在缓冲 i/o 请求中。 在下面的示例中，IOCTL 缓冲区包含指向大整数结构的嵌入指针 \_ 。

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;0

#define COUNT_FUNCTION 1
#define IOCTL_GETCOUNT CTL_CODE(FILE_DEVICE_UNKNOWN, \
            COUNT_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

与 \_ 上面所述的 IOCTL 和 FSCTL 缓冲区指针一样，嵌入在缓冲 i/o 请求中的指针也直接从用户模式应用程序传递到内核模式驱动程序。 对这些指针不执行任何验证。 因此，在可以安全取消引用嵌入指针之前，必须先调用 [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread) 或 [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)（括在 **try/except** 块中）。

如前面的示例所示，假设32位应用程序已为 **pDeviceCount**传递了有效值，则 \_ **pDeviceCount** 指向的大整数结构将在4字节边界上对齐。 **ProbeForRead** 和 **ProbeForWrite** 对照 *对齐* 参数的值（在本例中为 \_ (大整数) 的类型对齐）检查此对齐方式 \_ 。 在 x86 平台上，此宏表达式返回4个 (字节) 。 但在基于 Itanium 的计算机上，它返回8，导致 **ProbeForRead** 或 **ProbeForWrite** 引发状态 \_ 数据类型不 \_ 一致异常。

可以通过以下方式解决此问题：使大整数结构的正确对齐副本 \_ （如解决方案1中的副本）或使用未对齐的宏（如下所示）：

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER UNALIGNED *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;
```

 

