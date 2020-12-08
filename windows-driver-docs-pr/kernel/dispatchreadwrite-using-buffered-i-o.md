---
title: 使用缓冲 I/O 执行 DispatchReadWrite
description: 使用缓冲 I/O 执行 DispatchReadWrite
keywords:
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE i/o 函数代码
- IRP_MJ_READ i/o 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读取/写入调度例程
- 缓冲 i/o WDK 内核
- I/o WDK 内核，已缓冲
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1e7200dc4ff91d55d61dbbf193fed35e7fc3b6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833453"
---
# <a name="dispatchreadwrite-using-buffered-io"></a>使用缓冲 I/O 执行 DispatchReadWrite





为缓冲 i/o 设置其设备对象的任何最低级别设备驱动程序都通过将从其设备传输的数据返回到已锁定的系统空间缓冲区 **（位于 Irp &gt;AssociatedIrp.SystemBuffer）** 来满足读取请求。 它通过将数据从同一缓冲区传输到其设备来满足写入请求。

因此，此类设备驱动程序的 *DispatchReadWrite* 例程通常会在收到传输请求时执行以下操作：

1.  调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) 并确定传输请求的方向。

2.  检查请求的参数的有效性。

    -   对于读取请求，例程通常会检查驱动程序的 *IoStackLocation* - &gt; **参数**，以确定缓冲区是否足够大以接收从设备传输的数据。

        例如，系统键盘类驱动程序处理从 Win32 用户输入线程发出的读取请求。 此驱动程序定义了一个结构、键盘 \_ 输入 \_ 数据（用于存储来自设备的键击），并且在任何给定时刻将这些结构保存在内部环形缓冲区中，以便满足传入请求的要求。

    -   对于写入请求，例程通常会检查 temBuffer 中的值，并检查 **&gt;AssociatedIrp.SysIrp** 下的数据，如 **有必要，** 请检查是否存在有效性：也就是说，如果其设备仅接受包含具有定义的值范围的成员的结构化数据包，则为。

3.  如果任何参数无效， *DispatchReadWrite* 例程会立即完成 irp，如 [完成 irp](completing-irps.md)中所述。 否则，例程会将 IRP 传递到，以供其他驱动程序例程进一步处理，如将 [irp 向下传递到驱动程序堆栈](passing-irps-down-the-driver-stack.md)中所述。

使用缓冲 i/o 的最低级别设备驱动程序通常必须通过读取或写入由请求的发起方指定的大小的数据来满足传输请求。 此类驱动程序很有可能定义传入或发送到其设备的数据的结构，并且可能会在内部缓存结构化数据，因为系统键盘类驱动程序。

内部缓冲数据的驱动程序应支持 [**irp \_ mj \_ 刷新 \_ 缓冲区**](./irp-mj-flush-buffers.md) 请求，还可以支持 [**irp \_ mj \_ 关闭**](./irp-mj-shutdown.md) 请求。

链中的最高层驱动程序通常负责检查输入 IRP 的参数，然后将读取/写入请求传递到较低的驱动程序。 因此，许多较低级别的驱动程序可以假定读/写 IRP 中的 i/o 堆栈位置具有有效的参数。 如果链中的最低级别驱动程序知道数据传输的特定于设备的约束，则需要该驱动程序来检查其 i/o 堆栈位置中参数的有效性。

 

