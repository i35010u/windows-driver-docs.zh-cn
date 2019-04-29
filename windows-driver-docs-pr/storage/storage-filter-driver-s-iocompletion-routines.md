---
title: 存储筛选器驱动程序的 IoCompletion 例程
description: 存储筛选器驱动程序的 IoCompletion 例程
ms.assetid: 1a27598b-7113-4f95-8777-bbb10003c268
keywords:
- 存储筛选器驱动程序 WDK IoCompletion
- 筛选器驱动程序 WDK 存储 IoCompletion
- SFD WDK 存储 IoCompletion
- IoCompletion
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d18d425c8c46df374646f0568f89bce6069909e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362711"
---
# <a name="storage-filter-drivers-iocompletion-routines"></a>存储筛选器驱动程序的 IoCompletion 例程


## <span id="ddk_storage_filter_drivers_iocompletion_routines_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_IOCOMPLETION_ROUTINES_KG"></span>


存储筛选器驱动程序的[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)较低级驱动程序 （端口、 类和其他筛选器驱动程序，如果有） 已调用时调用例程[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。 *IoCompletion*例程存储筛选器驱动程序 (SFD) 应返回**状态\_详细\_处理\_必需**以防止完成处理驱动程序分配的 IRP，或如果 SFD 将重复 IRP 使用它在完成之前保留原始 IRP。

像其他任何更高级别的驱动[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) SFD 例程负责调用[ **IoFreeIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549113)以释放任何IRP 驱动程序*调度*例程使用创建[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)或者[ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310).

具体取决于其设备，可能会提供 SFD [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程的 Irp 它将发送到的下一步低驱动程序从其*调度*例程。 具体而言，检索并处理非标准格式的数据的设备可能需要具有 SFD *TranslateDataIn*例程调用从其*IoCompletion*例程的传输请求从这类设备到系统内存。

请注意，此类*TranslateDataIn*例程会调用在 IRQL = = 调度\_级别和在任意线程上下文中。 因此，在其中驱动程序返回数据的缓冲区必须位于非分页缓冲池或必须锁定和可访问使用映射，非分页的系统空间的虚拟地址。 有关安全地访问引发 IRQL 中用户提供的缓冲区的详细信息，请参阅[方法的访问数据缓冲区](https://msdn.microsoft.com/library/windows/hardware/ff554436)。

一般情况下，存储筛选器驱动程序应提供[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程替换为类驱动程序的相同的功能*IoCompletion*例程的 Irp，筛选器驱动程序使用 Srb 和 Cdb 设置。 因此，存储筛选器驱动程序可能具有的任意或全部*ReleaseQueue*， *InterpretRequestSense*，或*RetryRequest*可以从调用的例程存储类驱动程序*IoCompletion*例程。

有关详细信息*InterpretRequestSense*， *RetryRequest*，并*ReleaseQueue*例程，请参阅[存储类驱动程序](storage-class-drivers.md). 有关的常规要求的详细信息[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，请参阅[使用 IoCompletion 例程](https://msdn.microsoft.com/library/windows/hardware/ff565398)。

 

 




