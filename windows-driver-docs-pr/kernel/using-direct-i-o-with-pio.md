---
title: 将直接 I/O 与 PIO 配合使用
description: 将直接 I/O 与 PIO 配合使用
ms.assetid: 84d36567-c8c6-4576-91a0-829c8819de4d
keywords:
- 直接 i/o WDK 内核
- 缓冲 WDK i/o，直接 i/o
- 数据缓冲区 WDK i/o，直接 i/o
- I/o WDK 内核，直接 i/o
- PIO 传输操作 WDK 内核
- 程控 i/o 传输 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bab1c82565ac6bbc4c502feb97411ed2bd92fe36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838365"
---
# <a name="using-direct-io-with-pio"></a>将直接 I/O 与 PIO 配合使用





使用程控 i/o （PIO）而不是 DMA 的驱动程序必须将用户空间缓冲区双向映射到系统空间地址范围。 下图说明了 i/o 管理器如何为使用直接 i/o 的 PIO 传输操作设置[**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)请求。

![说明使用 pio 的设备的直接 i/o 的示意图](images/3mdlpio.png)

此图显示了使用 PIO 的设备如何处理相同的任务。

1.  某些范围的用户空间虚拟地址表示当前线程的缓冲区，该缓冲区的内容实际存储在一定数量的物理上不连续的页上。 如果缓冲区长度不为零，则 i/o 管理器会创建一个 MDL 来描述此缓冲区。

2.  I/o 管理器为当前线程的读取请求提供服务，该请求为其传递了一个表示缓冲区的用户空间虚拟地址范围。

3.  I/o 管理器或 FSD 检查用户提供的缓冲区的可访问性。 如果 i/o 管理器创建了一个 MDL，则它将使用 MDL 调用[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) ，该 mdl 指定用户缓冲区的虚拟地址范围。 **MmProbeAndLockPages**还会在 MDL 中填充相应的物理地址范围。

4.  I/o 管理器提供一个指向 IRP （**MdlAddress**）的指针，该 MDL 请求传输操作。 在驱动程序完成 IRP 后，在 i/o 管理器或文件系统调用[**MmUnlockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)之前，MDL 中描述的物理页面将保持锁定状态并分配给缓冲区。 但是，即使在将 IRP 发送到设备驱动程序或可能会分层到设备驱动程序的任何中间驱动程序之前，此类 MDL 中的虚拟地址也会变得不可见（和无效）。

5.  如果驱动程序需要系统（虚拟）地址，则驱动程序将使用 IRP 的**MdlAddress**指针调用[**MMGETSYSTEMADDRESSFORMDLSAFE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，将 MDL 中的用户空间虚拟地址映射到系统空间地址范围。 在上图中，AliasBuff 表示描述双重映射地址的 MDL。

6.  驱动程序使用双重映射 MDL （AliasBuff）中的系统空间虚拟地址范围将数据读入内存中。

当驱动程序通过调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)完成 IRP 后，如果驱动程序名为**MmGetSystemAddressForMdlSafe**，则 i/o 管理器或文件系统将释放 MDL 的双重映射系统空间范围。 I/o 管理器或文件系统会解除对 MDL 中所述页面的锁定，并在代表驱动程序上处置 MDL 和 IRP。 为了获得更好的性能，如步骤3中所述，驱动程序应避免双重映射 MDL 物理地址到系统空间，除非它们必须使用虚拟地址。 这样做将不必要地使用系统页表项，并可以降低驱动程序的性能和可伸缩性。 此外，如果系统超出页面表项，则系统可能会崩溃，因为大多数旧驱动程序无法处理这种情况。

当前用户线程的缓冲区和线程本身仅在线程是最新的情况下，才能在物理内存中驻留。 对于上图中显示的线程，在运行另一个进程的线程时，其用户缓冲区的内容可能会被分页到辅助存储。 当另一个进程的线程运行时，可以覆盖请求线程缓冲区的系统物理内存，除非内存管理器已锁定并保留包含原始线程缓冲区的相应物理页。

但是，当另一个线程为当前线程时，其缓冲区的原始线程的虚拟地址不会保持可见，即使内存管理器保留了缓冲区的物理页。 因此，驱动程序不能使用由[**MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)返回的虚拟地址来访问内存。 此例程的调用方必须将其结果传递给[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) （连同 IRP 的**MdlAddress**指针），才能使用基于数据包的系统或 bus 主机 DMA 传输数据。

 

 




