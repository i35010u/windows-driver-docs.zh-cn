---
title: 缓冲区处理
description: 缓冲区处理
ms.assetid: 0739ff35-2915-4237-9fe0-11559eccb0bb
keywords:
- 安全 WDK 文件系统，最大限度地减少威胁
- 缓冲 WDK 文件系统
- 分页缓冲 WDK 文件系统
- 非分页缓冲 WDK 文件系统
- bug 检查 WDK 文件系统
- 验证 WDK 文件系统
- 快速 i/o WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85bc7d2135cfb25c4a93f612db6aa6e2a57eef36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841480"
---
# <a name="buffer-handling"></a>缓冲区处理


## <span id="ddk_buffer_handling_if"></span><span id="DDK_BUFFER_HANDLING_IF"></span>


可能是任何驱动程序中的最常见错误都与缓冲处理无效或太小的缓冲区处理相关。 这些错误可能导致缓冲区溢出或导致系统崩溃，这会对系统造成安全损害。

从驱动程序的角度来看，缓冲区采用以下两种种类之一：

-   分页缓冲区，可能驻留在内存中，也可能不在内存中。

-   非分页缓冲区，必须驻留在内存中。

当然，无效的地址既未分页也未分页，但当操作系统开始处理错误（例如缓冲区的错误）时，它会将无效的地址隔离到 "标准" 地址范围（分页内核地址）之一中。非分页内核地址或用户地址，并引发相应类型的错误。 缓冲区错误始终由错误检查（例如，页面\_错误\_在\_非分页\_区域中）或异常（例如，状态\_访问\_冲突）处理。 对于 bug 检查，系统将暂停操作。 如果发生异常，将调用基于堆栈的异常处理程序，如果这些异常处理程序均未处理异常，则会调用 bug 检查。

无论如何，导致驱动程序出现错误检查的应用程序可能调用的任何访问路径都是驱动程序中的安全冲突。 这样，应用程序便可以导致整个系统的拒绝服务攻击。

此方面最常见的问题之一是驱动程序编写人员对操作环境的讨论太多。 这可能包括：

-   检查地址中是否设置了高位。 这不适用于基于 x86 的计算机，其中系统使用四 Gb 优化（4GT），方法是在 Boot.ini 文件中设置/3GB 选项。 在这种情况下，用户模式地址设置为地址空间的第三个千兆字节（GB）的高位。

-   使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)和[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)验证地址。 虽然这将确保地址在探测时是有效的用户模式地址，但没有任何要求它在探测操作后保持有效的方式。 因此，此技术引入了一个微妙的争用条件，这可能会导致定期遇到再现崩溃。 出于不同的原因，需要**ProbeForRead**和**ProbeForWrite**调用：验证地址是否为用户模式地址，以及缓冲区的长度是否在用户地址范围内。 如果省略探测，用户可以传入有效的内核模式地址，这将不会被 \_\_尝试并 \_\_除外（结构化异常处理），并将打开一个大型安全漏洞。 因此，需要**ProbeForRead**和**ProbeForWrite**调用以确保对齐，并且用户模式地址加上长度在用户地址范围内。 但是，\_\_尝试 \_\_除需要阻止访问以外的块。

    请注意， [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)仅验证地址和长度是否在可能的用户模式地址范围内（例如，对于没有4gt 的系统，稍微小于 2 GB），而不验证内存地址是否有效。 相反， [**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)将尝试访问指定长度的每页中的第一个字节，以验证它们是否为有效的内存地址。

-   依赖于内存管理器函数（例如[**MmIsAddressValid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmisaddressvalid)）来确保地址有效。 与探测函数一样，这会引入可能导致遇到再现崩溃的争用情况。

-   未能使用结构化异常处理。 \_\_try 和 \_\_除编译器内的函数外，使用操作系统级的异常处理支持。 通过调用[**ExRaiseStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)或相关函数之一，引发内核级别的异常。 驱动程序无法在可能引发异常的调用周围使用结构化异常处理会导致 bug 检查（通常是 KMODE\_异常\_未\_处理）。

    请注意，在不应引发错误的代码周围使用结构化异常处理是错误的。 这只会掩盖可能会找到的实际 bug。 将 \_\_尝试并 \_\_在您的例程的最高调度级别除外，不是此问题的正确解决方案，尽管有时驱动程序编写器会尝试使用反射解决方案。

-   依赖于剩余的用户内存内容。 例如，假设驱动程序要将值写入用户模式内存位置，稍后在同一例程中引用该内存位置。 恶意应用程序可能会主动修改该内存，因此会导致驱动程序崩溃。

对于文件系统，这些问题特别严重，因为它们通常依赖于直接访问用户缓冲区（方法\_传输方法）。 此类驱动程序会直接操作用户缓冲区，因此必须包含用于缓冲处理的预防措施，以避免操作系统级崩溃。 快速 i/o 始终传递原始内存指针，因此，如果支持快速 i/o，驱动程序需要防范类似的问题。

WDK 包含 FASTFAT 和 CDFS 文件系统示例代码中的大量缓冲区验证示例，包括：

-   Fastfat**中的** **FatLockUserBuffer**函数\\deviosup 使用[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)锁定用户缓冲区后面的物理页面[ **，并使用 MmGetSystemAddressForMdlSafe FatMapUserBuffer 创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)虚拟锁定的页的映射。

-   Fastfat 中的**FatGetVolumeBitmap**函数\\Fsctl 使用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)和[**PROBEFORWRITE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)来验证碎片整理 API 中的用户缓冲区。

-   Cdfs 中的**CdCommonRead**函数\\读取。 c 使用 \_\_尝试，并 \_\_除了代码之外的任何用户缓冲区。 请注意， **CdCommonRead**中的示例代码显示使用 "try" 和 "except" 关键字。 在 WDK 环境下，C 中的这些关键字是根据编译器扩展定义的，\_\_try 和 \_\_除外。 使用C++代码的任何人都必须使用本机编译器类型来正确处理异常，因为\_\_try C++是关键字，但不是 C 关键字，将提供对内核驱动C++程序无效的异常处理形式。

 

 




