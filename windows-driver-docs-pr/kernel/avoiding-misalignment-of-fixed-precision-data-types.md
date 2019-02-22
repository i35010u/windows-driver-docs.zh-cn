---
title: 避免未对齐的固定精度的数据类型
description: 避免未对齐的固定精度的数据类型
ms.assetid: 4e214bd8-b622-447a-b484-bd1d5d239de7
keywords:
- 文件系统控制代码 WDK 64 位
- FSCTL WDK 64 位
- 控制代码 WDK 64 位
- I/O 控制代码 WDK 内核，在 64 位驱动程序中的 32 位 I/O
- Ioctl WDK 内核，在 64 位驱动程序中的 32 位 I/O
- 指针精确度 WDK 64 位
- 固定精度数据类型 WDK 64 位
- 未对齐的固定精度数据类型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384f999800faef2e74e0252c0fdd3c6100cdd2f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524298"
---
# <a name="avoiding-misalignment-of-fixed-precision-data-types"></a>避免未对齐的固定精度的数据类型





遗憾的是，很可能具有相同的大小，但不同的对齐要求，为 32 位和 64 位编程的数据类型。 因此不是所有 IOCTL/FSCTL 缓冲区未对齐问题可以都避免通过更改指针精确度的数据类型为固定精度的类型。 这意味着，内核模式驱动程序 Ioctl 和 FSCTLs 传递包含某些固定精度的数据类型 （或者指向它们） 缓冲区还可能需要将 thunked。

### <a name="which-data-types-are-affected"></a>受影响的数据类型

此问题会影响固定精度的数据类型本身是结构。 这是因为用于确定结构的对齐要求的规则是特定于平台的。

例如，  **\_ \_int64**大型\_整数和 KFLOATING\_保存必须在 x86 上的 4 字节边界上对齐的平台。 但是，在基于 Itanium 的计算机，它们必须对齐 8 字节边界上。

若要确定在特定平台上给定的数据类型的对齐要求，请使用**类型\_对齐**宏在该平台上的。

### <a name="how-to-fix-the-problem"></a>如何解决此问题

在以下示例中，IOCTL 是一种方法\_既不 IOCTL，因此**Irp-&gt;UserBuffer**指针传递到内核模式驱动程序的用户模式应用程序直接从。 Ioctl 和 FSCTLs 中使用的缓冲区上不执行任何验证。 因此调用[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)或[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)是必需的才能安全地取消引用缓冲区指针。

假设 32 位应用程序已通过有效的值**Irp-&gt;UserBuffer**，大\_指向整数结构**p-&gt;DeviceTime**将在 4 字节边界上对齐。 **ProbeForRead**检查传入的值针对这种调整其*对齐*参数，在这种情况下即**类型\_对齐**(大\_整数)。 在 x86 平台，则此宏表达式返回 4 （字节）。 但是，在基于 Itanium 的计算机，它返回 8，导致**ProbeForRead**引发状态\_数据类型\_不对齐异常。

**请注意**  删除**ProbeForRead**调用仍然无法解决问题，但仅会使它很难诊断。

 

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

以下部分介绍如何解决上述问题。 请注意为了简便起见，已进行了编辑所有代码片段。

### <a name="solution-1-copy-the-buffer"></a>解决方案 1：将缓冲区复制

为了避免出现不一致问题的最安全方法是缓冲区的访问其内容，如以下示例所示之前创建副本。

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

此解决方案可以优化为更好的性能通过先检查是否正确对齐缓冲区内容。 如果是这样，可以原样使用缓冲区。 否则，该驱动程序创建缓冲区的副本。

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

### <a name="solution-2-use-the-unaligned-macro"></a>解决方案 2:使用未对齐的宏

**未对齐**宏告知 C 编译器生成的代码都可以访问**DeviceTime**字段而无需使对齐错误。 请注意，在基于 Itanium 的平台上使用此宏有可能使您的驱动程序，明显更大和较慢。

```cpp
typedef struct _IOCTL_PARAMETERS2 {
    LARGE_INTEGER DeviceTime;
} IOCTL_PARAMETERS2;
typedef IOCTL_PARAMETERS2 UNALIGNED *PIOCTL_PARAMETERS2;
```

### <a name="pointers-are-also-affected"></a>指针也会受到影响

前面所述的不一致问题也可能发生在缓冲 I/O 请求。 在以下示例中，IOCTL 缓冲区包含嵌入式的指针到大型\_整数结构。

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;0

#define COUNT_FUNCTION 1
#define IOCTL_GETCOUNT CTL_CODE(FILE_DEVICE_UNKNOWN, \
            COUNT_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

等方法\_既不 IOCTL 和 FSCTL 缓冲区指针前面所述，直接从用户模式应用程序到内核模式驱动程序还传递指针嵌入在缓冲 I/O 请求。 这些指针上不执行任何验证。 因此调用[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)或[ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)中括起来，**试用 / 除外**块中，是嵌入式的指针可以为安全地取消引用之前，需要。

如前面的示例，假设 32 位应用程序已为传递有效的值中所示**pDeviceCount**，大型\_指向整数结构**pDeviceCount**将 4-上对齐字节边界。 **ProbeForRead**并**ProbeForWrite**检查此对齐方式的值*对齐*参数，在这种情况下即类型\_对齐方式 (大\_整数）。 在 x86 平台，则此宏表达式返回 4 （字节）。 但是，在基于 Itanium 的计算机，它返回 8，导致**ProbeForRead**或**ProbeForWrite**引发状态\_数据类型\_不对齐异常。

可解决此问题会将正确对齐的大型副本\_整数结构，如下所示的解决方案 1，或通过使用未对齐的宏，如下所示：

```cpp
typedef struct _IOCTL_PARAMETERS3 {
    LARGE_INTEGER UNALIGNED *pDeviceCount;
} IOCTL_PARAMETERS3, *PIOCTL_PARAMETERS3;
```

 

 




