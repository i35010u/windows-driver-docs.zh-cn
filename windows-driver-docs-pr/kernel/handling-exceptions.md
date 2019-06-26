---
title: 处理异常
description: 处理异常
ms.assetid: 20040d86-5088-48ec-a5b9-54760d143871
keywords:
- 结构化的异常处理 WDK 内核
- 异常 WDK 内核
- 访问冲突 WDK 内核
- 硬件定义的异常 WDK 内核
- 软件定义的异常 WDK 内核
- 错误 WDK 内核
- 保护页冲突 WDK 内核
- 页读取错误 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 466ea89782b7b795fb0a81e3d995f43ac72fe9f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386881"
---
# <a name="handling-exceptions"></a>处理异常





操作系统使用结构化的异常处理以指示特定类型的错误。 由驱动程序调用的例程可以引发该驱动程序必须处理的异常。

系统捕获以下常规类型的异常：

1.  硬件定义的错误或陷阱，例如，

    -   访问冲突 （见下文）
    -   （例如为奇数字节边界上对齐的 16 位实体） 的数据类型 misalignments
    -   非法和特权指令
    -   无效的锁定序列 （尝试执行无效的代码的互锁部分中的说明序列）
    -   整数被零除和溢出
    -   浮点除以零、 溢出、 下溢和保留的操作数
    -   断点和单步执行 （以支持调试器）

2.  系统软件定义的异常，例如，

    -   保护页冲突 （尝试加载或存储数据来自或发往一个保护页内的位置）
    -   （尝试页读入内存并遇到了并发的 I/O 错误） 的页读取错误

*访问冲突*尝试执行的操作不允许使用当前的页保护设置的页面上。 在以下情况下，发生访问冲突：

-   一个无效的读取或写入操作，例如写入到只读的页。

-   若要访问超过当前程序的地址空间 （称为长度违规） 的限制的内存。

-   若要访问但专用于系统组件使用的是当前驻留的页。 例如，用户模式代码是不允许访问内核正在使用的页。

如果某项操作可能会导致异常，该驱动程序应将中的操作**试用 / 除外**块。 在用户模式下的位置的访问是典型引发异常的原因。 例如， [ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)例程检查驱动程序可以实际写入到用户模式缓冲区。 如果不能则例程将引发状态\_访问\_冲突异常。 在下面的代码示例，该驱动程序将调用**ProbeForWrite**中**试用 / 除外**，以便它可以处理所产生的异常，如果其中一个应发生。

```cpp
try {
    ...
    ProbeForWrite(Buffer, BufferSize, BufferAlignment);
 
    /* Note that any access (not just the probe, which must come first,
     * by the way) to Buffer must also be within a try-except.
     */
    ...
} except (EXCEPTION_EXECUTE_HANDLER) {
    /* Error handling code */
    ...
}
```

驱动程序必须处理任何引发的异常。 未处理的异常导致了系统的 bug 检查。 要引发的异常将导致该驱动程序必须处理它： 较低级驱动程序不能依赖于更高级别的驱动程序处理异常。

驱动程序可以直接通过引发异常， [ **ExRaiseAccessViolation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraiseaccessviolation)， [ **ExRaiseDatatypeMisalignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraisedatatypemisalignment)，或[**ExRaiseStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exraisestatus)例程。 该驱动程序必须处理这些例程引发任何异常。

下面是例程，至少在某些情况下，将引发异常的部分列表：

-   [**MmMapLockedPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpages)

-   [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)

-   [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)

-   [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)

对用户模式缓冲区的内存访问也会导致访问冲突。 有关详细信息，请参阅[中引用用户空间地址错误](errors-in-referencing-user-space-addresses.md)。

请注意，不同于结构化的异常处理C++异常。 内核不支持C++异常。

有关结构化异常处理的详细信息，请参阅 Microsoft Windows SDK 和 Visual Studio 文档。

 

 




