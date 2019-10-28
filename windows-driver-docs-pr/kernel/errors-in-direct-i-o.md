---
title: 直接 I/O 出错
description: 直接 I/O 出错
ms.assetid: 9efc2875-3402-4e2e-871b-3cc1d8f45360
keywords:
- 可靠性 WDK 内核，直接 i/o
- 直接 i/o WDK 内核
- I/o WDK 内核，直接 i/o
- 长度为零的缓冲区 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038f851bec4bebd301cda6aee62b93ce61749679
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838707"
---
# <a name="errors-in-direct-io"></a>直接 I/O 出错





最常见的直接 i/o 问题是无法正确处理长度为零的缓冲区。 因为 i/o 管理器不会为长度为零的传输创建 MDLs，所以，长度为零的缓冲区将导致**Irp&gt;MdlAddress**的值**为 NULL** 。

若要映射地址空间，驱动程序应使用[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，如果映射失败，则它将返回 null，因为如果驱动程序传递**NULL** **MdlAddress**，则会返回**null** 。 在尝试使用返回的地址之前，驱动程序应始终检查**NULL 返回值**。

直接 i/o 涉及将用户的地址空间双倍映射到系统地址缓冲区，以便两个不同的虚拟地址具有相同的物理地址。 双重映射具有以下后果，这可能会导致驱动程序出现问题：

-   用户地址的虚拟页中的偏移量成为系统页中的偏移量。

    超出这些系统缓冲区末尾的访问可能会在很长一段时间内出现，具体取决于映射的页面粒度。 除非在页的末尾附近分配了调用方的缓冲区，否则超出缓冲区末尾的数据仍会出现在缓冲区中，并且调用方将不知道是否发生了任何错误。 如果缓冲区的末尾与页的末尾一致，则结束时的系统虚拟地址可能指向任何内容或可能无效。 此类问题可能非常难以找到。

-   如果调用进程有另一个修改了用户映射内存的线程，则当用户的内存映射更改时，系统缓冲区的内容会更改。

    在这种情况下，使用系统缓冲区来存储暂存数据可能会导致问题。 同一内存位置中的两个提取可能产生不同的值。

    下面的代码段接收直接 i/o 请求中的字符串，然后尝试将该字符串转换为大写字符：

    ```cpp
    PWCHAR  PortName = NULL;

    PortName = (PWCHAR)MmGetSystemAddressForMdlSafe(irp->MdlAddress, NormalPagePriority);

    //
    // Null-terminate the PortName so that RtlInitUnicodeString will not
    // be invalid.
    //
    PortName[Size / sizeof(WCHAR) - 1] = UNICODE_NULL;

    RtlInitUnicodeString(&AdapterName, PortName);
    ```

    由于缓冲区的格式可能不正确，因此代码会尝试强制将 Unicode **NULL**作为最后一个缓冲区字符。 但是，如果基础物理内存是双重映射到用户和内核模式地址的，则该进程中的另一个线程可以在此写入操作完成后立即覆盖缓冲区。

    相反，如果不存在**NULL 值**，则对**RtlInitUnicodeString**的调用可能会超出缓冲区的范围，并且可能会导致 bug 检查（如果它在系统映射之外）。

如果驱动程序创建并映射其自己的 MDL，应确保它仅使用已探测的方法访问 MDL。 也就是说，当驱动程序调用[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)时，它将指定访问方法（**IoReadAccess**、 **IoWriteAccess**或**IoModifyAccess**）。 如果驱动程序指定了**IoReadAccess**，则它不能再尝试写入[**MmGetSystemAddressForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemaddressformdl)或[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)提供的系统缓冲区。

 

 




