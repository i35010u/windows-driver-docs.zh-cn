---
title: 直接 I/O 出错
description: 直接 I/O 出错
ms.assetid: 9efc2875-3402-4e2e-871b-3cc1d8f45360
keywords:
- 可靠性 WDK 内核，直接 I/O
- 直接 I/O WDK 内核
- I/O WDK 内核，直接 I/O
- 长度为零的缓冲区 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ed8c1e26df36f609ddabb8d1b2e94853ba31ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385127"
---
# <a name="errors-in-direct-io"></a>直接 I/O 出错





最常见的直接 I/O 问题无法正确处理的缓冲区长度为零。 因为 I/O 管理器不会为长度为零的传输创建 MDLs，长度为零的缓冲区会导致**NULL**时的值**Irp-&gt;MdlAddress**。

若要映射的地址空间，驱动程序应使用[ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，它将返回**NULL**如果映射失败，因为它将驱动程序通过了如果**NULL** **MdlAddress**。 驱动程序应始终检查**NULL**返回之前尝试使用返回的地址。

直接 I/O 涉及双映射到系统地址缓冲区，用户的地址空间，以便两个不同的虚拟地址具有相同的物理地址。 双映射会产生以下影响，有时会导致驱动程序的问题：

-   用户的地址的虚拟页中的偏移量将成为到系统页的偏移量。

    为长一段时间，具体取决于映射页粒度，这些系统缓冲区的末尾之外的访问可能会被忽略。 除非调用方的缓冲区分配页末尾附近，超出缓冲区末尾写入数据不过会显示在缓冲区，并调用方将不会察觉发生任何错误。 如果与页的最终一致的缓冲区的末尾，超出末尾位置的系统虚拟地址可以指向任何内容，或者可能无效。 可以极其困难，若要查找此类问题。

-   如果调用进程已修改用户的映射的内存的另一个线程，当用户的内存映射发生更改时将更改系统缓冲区的内容。

    在此情况下，使用系统缓冲区来存储临时数据会导致问题。 从相同的内存位置的两个提取操作可能会产生不同的值。

    以下代码段在直接 I/O 请求中，接收一个字符串，然后尝试将该字符串为大写字符转换：

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

    缓冲区可能格式不正确，因为代码尝试强制 Unicode **NULL**作为最后一个缓冲区的字符。 但是，如果基础物理内存双向映射到用户-和内核模式地址，在过程中的另一个线程可以覆盖在此写操作完成后立即缓冲区。

    相反，如果**NULL**不存在，则调用**RtlInitUnicodeString**可以超过缓冲区的范围，并且如果它在外部系统映射可能会导致的 bug 检查。

如果驱动程序创建并映射其自身 MDL，应确保它仅使用方法，它具有为其探测访问 MDL。 也就是说，当驱动程序调用[ **MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)，它指定访问方法 (**IoReadAccess**， **IoWriteAccess**，或**IoModifyAccess**)。 如果指定了该驱动程序**IoReadAccess**，它必须稍后尝试写入到可通过系统缓冲区[ **MmGetSystemAddressForMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemaddressformdl)或[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)。

 

 




