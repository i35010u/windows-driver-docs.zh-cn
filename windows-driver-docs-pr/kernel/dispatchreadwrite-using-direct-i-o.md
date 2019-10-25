---
title: 使用直接 I/O 执行 DispatchReadWrite
description: 使用直接 I/O 执行 DispatchReadWrite
ms.assetid: 5174fe1f-aee5-4c8a-87a1-7f185ed4e242
keywords:
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE i/o 函数代码
- IRP_MJ_READ i/o 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读取/写入调度例程
- 直接 i/o WDK 内核
- I/o WDK 内核，直接 i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c40e4aeb46846dec245a93629c59885867b48dff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836838"
---
# <a name="dispatchreadwrite-using-direct-io"></a>使用直接 I/O 执行 DispatchReadWrite





为直接 i/o 设置其设备对象的任何较低级别的设备驱动程序都通过返回从其设备传输到系统物理内存的数据来满足读取请求，这是由**Irp&gt;MdlAddress**的 MDL 描述的。 它通过将数据从系统物理内存传输到设备来满足写入请求。

较低级别的驱动程序必须异步处理读/写请求。 因此，每个较低级别的驱动程序的[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程必须通过[**irp\_mj\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)和[**irp\_mj\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)将具有有效参数的 irp 写入其他驱动程序例程，如[通过传递Irp 驱动程序堆栈](passing-irps-down-the-driver-stack.md)。

对于发送到较低级别驱动程序的读取/写入 Irp，已探测**Irp&gt;MdlAddress**的 MDL 描述的分页物理内存，以获取正确的访问权限，以便执行请求的传输并已由链中或 i/o 管理器中的最高级别的驱动程序。 为直接 i/o 设置其设备对象的任何中间或最低级别驱动程序都不应调用[**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) ，因为此操作已完成。 最低级别的驱动程序调用[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)。 （Windows 98 的驱动程序改为调用[**MmGetSystemAddressForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemaddressformdl) 。 Windows Me、Windows 2000 和更高版本的 Windows 的驱动程序应使用**MmGetSystemAddressForMdlSafe**。）

如果任何中间或最低级别的设备驱动程序的*DispatchReadWrite*例程在其 i/o 堆栈位置中都不能信任较高级别的驱动程序来仅向下传递包含有效参数的 irp，则应该验证其 i/o 堆栈位置中的参数。 如果*DispatchReadWrite*例程发现参数错误，它应按照[完成 irp](completing-irps.md)中所述的相应错误状态\_*XXX*值来完成 irp。 如果参数有效，则根据[高级驱动程序的 DispatchReadWrite 中](dispatchreadwrite-in-higher-level-drivers.md)的准则，中间驱动程序的*DispatchReadWrite*例程必须通过请求，以便进一步处理。

最低级别的设备驱动程序的*DispatchReadWrite*例程必须与传输请求一起调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，传递 IRP 以供其他驱动程序例程进一步处理，并返回状态\_挂起，如中[所述。将 Irp 沿驱动程序堆栈向下传递](passing-irps-down-the-driver-stack.md)。

请注意，设备驱动程序的*DispatchReadWrite*例程可以通过使用驱动程序确定的*密钥*值调用[**IoStartPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket) ，来控制 irp 在其设备上排队的顺序，以实现更快的 i/o 吞吐量。 稍后，驱动程序中的另一个例程会取消排队 IRP，确定是否必须将请求的长度拆分为部分传输操作，并计划设备传输数据。

通常，必须将大型传输请求拆分为满足其设备限制的设备驱动程序应推迟这些操作，直至设置给定传输请求所需的设备。 此类设备驱动程序的*DispatchReadWrite*例程不应在任何设备特定传输约束中检查传入 irp 的 i/o 堆栈位置，也不会尝试计算部分传输范围，当驱动程序可以将这些检查推迟到紧靠在其[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) （或其他驱动程序例程）之前，会对设备进行传输操作。

 

 




