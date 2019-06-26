---
title: 使用直接 I/O 执行 DispatchReadWrite
description: 使用直接 I/O 执行 DispatchReadWrite
ms.assetid: 5174fe1f-aee5-4c8a-87a1-7f185ed4e242
keywords:
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE I/O 函数代码
- IRP_MJ_READ I/O 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读/写调度例程
- 直接 I/O WDK 内核
- I/O WDK 内核，直接 I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f103532f75e9d852ce9f26e8e27c9376a5d866e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384976"
---
# <a name="dispatchreadwrite-using-direct-io"></a>使用直接 I/O 执行 DispatchReadWrite





设置了其设备对象的直接 I/O 通过返回的数据满足读取的请求任何更低级别的设备驱动程序从其设备传输到系统的物理内存，从而在 MDL 描述**Irp-&gt;MdlAddress**. 它通过将数据从出系统物理内存传输到其设备满足写入请求。

较低级别的驱动程序必须以异步方式处理读/写请求。 因此，每个较低级别驾[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程必须传递[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)并[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)带到其他驱动程序例程，如中所述的有效参数的 Irp[传递 Irp 关闭驱动程序堆栈](passing-irps-down-the-driver-stack.md)。

读/写 Irp 发送到较低级别的驱动程序，分页的物理内存所述的在 MDL **Irp-&gt;MdlAddress**具有已被探测以确定正确的访问权限的权限来执行请求的传输和具有已被锁定在链中的最高级别的驱动程序或 I/O 管理器。 任何中间或最低级别的驱动程序，用于设置其设备对象的直接 I/O 不应调用[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)由于这已完成。 最低级别驱动程序调用[ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)。 (Windows 98 的驱动程序调用[ **MmGetSystemAddressForMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemaddressformdl)相反。 Windows Me、 Windows 2000 和更高版本的 Windows 驱动程序应使用**MmGetSystemAddressForMdlSafe**。)

任何中间或最低级别的设备驱动程序*DispatchReadWrite*例程应验证的读/写 Irp 其 I/O 堆栈位置中的参数，如果它不能信任将向下仅使用有效的 Irp 传递的更高级别的驱动程序参数。 如果*DispatchReadWrite*例程发现参数错误时，它应完成因相应的错误状态 IRP\_*XXX*值，如前面所述[完成Irp](completing-irps.md)。 如果参数有效，中间驱动程序的*DispatchReadWrite*例程必须进行进一步处理，根据中的指导原则传递请求[Higher-Level 驱动程序中的DispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md).

最低级别的设备驱动程序*DispatchReadWrite*例程必须调用[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)与传输请求将传递 IRP 进行进一步处理由其他驱动程序例程，并返回状态\_PENDING，如中所述[驱动程序堆栈的下层传递 Irp](passing-irps-down-the-driver-stack.md)。

请注意，设备驱动程序*DispatchReadWrite*例程可以控制在其中 Irp 要排队发送至更快的 I/O 吞吐量其设备通过调用的顺序[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)与驱动程序确定*密钥*值。 驱动程序中的另一个例程 IRP 更高版本中取消排队、 确定是否为请求的长度必须将拆分为部分传输操作，和程序的设备将传输数据。

一般情况下，必须拆分大型传输请求，以满足其设备的限制的设备驱动程序应设置适用于给定的传输请求的设备之前，只需推迟到这些操作。 此类设备驱动程序的*DispatchReadWrite*例程应不检查对于任何特定于设备的传输约束，传入 Irp 的 I/O 堆栈位置也不会尝试时，驱动程序可以计算部分传输范围推迟直至这些检查其[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio) （或其他驱动程序例程） 程序传输操作中的设备。

 

 




