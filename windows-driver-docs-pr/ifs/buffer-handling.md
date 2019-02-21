---
title: 缓冲区处理
description: 缓冲区处理
ms.assetid: 0739ff35-2915-4237-9fe0-11559eccb0bb
keywords:
- 安全 WDK 文件系统、 最大程度减少威胁
- 缓冲区 WDK 文件系统
- 分页的缓冲区 WDK 的文件系统
- 非分页缓冲区 WDK 文件系统
- bug 检查 WDK 的文件系统
- 地址验证 WDK 文件系统
- 快速 I/O WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84d1c608fb47e03e842b8c3ac52af7a2b10f0815
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534322"
---
# <a name="buffer-handling"></a>缓冲区处理


## <span id="ddk_buffer_handling_if"></span><span id="DDK_BUFFER_HANDLING_IF"></span>


可能是任何驱动程序中最常见的错误与缓冲区的无效或太小的缓冲区处理。 这些错误可以允许缓冲区溢出或导致系统崩溃，构成系统的安全破坏。

从驱动程序的角度来看，缓冲区有两种类型之一：

-   分页缓冲区中可能也不是驻留在内存中。

-   非分页缓冲区，它必须是驻留在内存中。

当然，无效的地址是分页既非分页，但操作系统开始努力解决此类缓冲区的页错误导致，它将为一个"标准"地址范围 （分页的内核地址，隔离地址无效非分页内核地址或用户地址），并引发适当类型的错误。 缓冲区始终处理错误的 bug 检查通过 (页\_容错\_IN\_未分页\_区域，例如) 或异常情况 (状态\_访问\_冲突，例如)。 对于错误检查，系统将停止操作。 出现异常时，将通过调用基于堆栈的异常处理程序，如果其中任何一个处理异常，错误检查将在调用。

无论如何，不能调用由应用程序，使驱动程序导致的 bug 检查任何访问路径是在驱动程序中的安全冲突。 这允许应用程序会导致整个系统的拒绝服务攻击。

在此区域中最常见的问题之一是，驱动程序编写者都认为太多了解操作环境。 这可能包括：

-   正在检查在地址中，设置了高位。 这不会通过在 Boot.ini 文件中设置 /3GB 选项适用于基于 x86 的计算机的系统正在使用四个千兆字节调整 (4GT)。 在这种情况下，用户模式地址设置地址空间的第三个千兆字节 (GB) 的高位。

-   使用[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)并[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)以验证地址。 这将确保地址在探测时是有效的用户模式地址，而没有任何需要它来探测操作后仍然有效。 因此，这种技术引入可能会定期不可再现故障导致的细微的争用条件。 **ProbeForRead**并**ProbeForWrite**调用所需的不同的原因： 若要验证地址是否用户模式地址和缓冲区的长度是用户地址范围内。 如果省略探测，则用户可以在有效的内核模式地址，将不会捕获由中传递\_\_尝试并\_ \_except 块 （结构化的异常处理） 和将打开一个很大的安全漏洞。 因此**ProbeForRead**并**ProbeForWrite**调用所需确保对齐方式和用户模式地址，以及长度，是用户地址范围内。 但是， \_\_尝试并\_\_除了防止访问所需的块。

    请注意， [ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)仅验证可能的用户模式地址范围内 （略有小于 2 GB 的系统而 4GT，例如未)，地址和长度秋季不是否内存地址有效。 与此相反， [ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)将尝试访问以验证这些是有效的内存地址中指定的长度的每个页面中的第一个字节。

-   依赖于内存管理器功能 ([**MmIsAddressValid**](https://msdn.microsoft.com/library/windows/hardware/ff554572)，例如) 以确保地址是否有效。 与探测函数一样，它引入了不可再现故障可能会导致的争用条件。

-   若要使用结构化的异常处理的失败。 \_\_尝试并\_\_只是编译器中的函数用于异常处理使用操作系统级的支持。 通过调用重新引发在内核级别的异常[ **ExRaiseStatus**](https://msdn.microsoft.com/library/windows/hardware/ff545529)，或其中一个相关的函数。 无法使用结构化的异常处理任何可能会引发异常的调用周围的驱动程序将导致的 bug 检查 (通常 KMODE\_异常\_不\_HANDLED)。

    请注意，它使用结构化的异常处理预期不会引发错误的代码周围的错误。 这将只是掩码实际错误，否则可能会找到。 将放\_\_尝试并\_\_顶部调度级别的例程的包装器不是正确的解决方案，此问题，尽管它有时是由驱动程序编写器已尝试的反射解决方案除外。

-   依赖于剩余稳定的用户内存的内容。 例如，假定一个驱动程序要写入到用户模式内存位置的值，并更高版本中的相同例程参阅该内存位置。 恶意应用程序都可以主动修改该内存，并因此，会导致崩溃的驱动程序。

对于文件系统，这些问题都是特别严重由于它们通常依赖于直接访问用户缓冲区 (该方法\_既不传输方法)。 此类驱动程序直接处理用户缓冲区，并因此必须包含将缓冲区处理的预防性方法，以避免操作系统级别崩溃。 快速的 i/o 操作始终将传递原始内存的指针，因此驱动程序需要支持快速 I/O 时防止类似的问题。

WDK 包含许多缓冲区 FASTFAT 和 CDFS 文件系统的示例代码中，验证的示例包括：

-   **FatLockUserBuffer**函数中 fastfat\\deviosup.c 使用[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664)锁定用户缓冲区背后的物理页和[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)中**FatMapUserBuffer** ，创建的虚拟已锁定的页映射。

-   **FatGetVolumeBitmap**函数中 fastfat\\fsctl.c 使用[ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)并[ **ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)来验证用户缓冲区中的碎片整理 API。

-   **CdCommonRead**中的 cdf 函数\\read.c 使用\_\_尝试并\_\_到零个用户缓冲区的代码周围除外。 请注意，此示例中的代码**CdCommonRead**似乎使用 try 和 except 关键字。 在 WDK 环境中，这些关键字在 C 中的定义的编译器扩展方面\_\_尝试并\_\_除外。 使用 c + + 代码的任何人都必须使用本机编译器类型正确，处理异常作为\_ \_try 是 c + + 关键字，但不是 C 关键字，并将提供不是有效的内核驱动程序的 c + + 异常处理的一种形式。

 

 




