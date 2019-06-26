---
title: 存储类驱动程序的 BuildRequest 例程
description: 存储类驱动程序的 BuildRequest 例程
ms.assetid: 2ba26628-4862-440c-b8f1-dd983cf9923b
keywords:
- BuildRequest
- I/O 堆栈位置 WDK 存储
- 正在重试请求 WDK 存储
- SCSI 请求检测 WDK 存储
- 请求检测 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7587cc600364d89fb54b9f7544edcdaafbcefaba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368221"
---
# <a name="storage-class-drivers-buildrequest-routine"></a>存储类驱动程序的 BuildRequest 例程


## <span id="ddk_storage_class_drivers_buildrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_BUILDREQUEST_ROUTINE_KG"></span>


等所有更高级别的内核模式驱动程序存储类驱动程序必须设置为下一步低驱动程序的 IRP 的 I/O 堆栈位置时[处理请求存储外围设备](handling-requests-to-storage-peripherals.md)。 在类驱动程序设置了与 Srb 系统提供的端口驱动程序的 Irp，端口驱动程序的 I/O 堆栈位置使用以下设置：

-   **MajorFunction**包含 IRP\_MJ\_SCSI

-   **Parameters.Scsi.Srb**包含指向 SRB

每个类驱动程序负责 Srb 以及与它们使用的设置 Cdb 基础存储端口驱动程序分配内存。 在类驱动程序可以设置后备链列表为其 Srb **ExInitializeNPageLookasideList**或致电**ExAllocatePool**非分页内存。 请参阅[使用后备链列表](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-lookaside-lists)有关使用后备链列表和非分页缓冲的池的详细信息。

是否从池或驱动程序创建后备链列表，它分配内存，每个存储类驱动程序负责释放 Srb 为其分配的内存。 存储类驱动程序*IoCompletion*例程中, 所述[存储类驱动程序 IoCompletion 例程](storage-class-driver-s-iocompletion-routines.md)，通常发布回后备链列表为 Srb 分配的内存。

类驱动程序*BuildRequest*例程必须 SRB 成员，包括它设置为其设备与通信 CDB 长度中设置适当的值。 对于返回请求检测信息和/或驱动程序可能需要重试的请求，它会设置*IoCompletion*例程中。 用于读取或写入请求，它 ORs **SrbFlags**具有适当的传输方向，SRB\_标志\_数据\_IN 或 SRB\_标志\_数据\_签出，分别。

一个*BuildRequest*例程可能会共享负责设置与一对 SRB *SendSrbSynchronous*并*SendSrbAsynchronous*例程。 即*BuildRequest*例程可以设置通常设置的所有请求的 SRB 成员时*SendSrbXxx*例程每个设置 SRB 值只涉及每种类型的请求。 当 IRP 传递给该端口驱动程序从*SendSrbAsynchronous*例程，IRP 必须使用设置驱动程序提供*IoCompletion*例程。

类驱动程序加载后，它会设置大多数 Srb**函数**成员设置为 SRB\_函数\_EXECUTE\_SCSI、，该值指示通过总线发送的设备 I/O 请求。

有关系统定义的 SRB 成员及其值的详细信息，请参阅[ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)。

### <a name="span-idsettingupsrbsforrequestsensespanspan-idsettingupsrbsforrequestsensespanspan-idsettingupsrbsforrequestsensespansetting-up-srbs-for-request-sense"></a><span id="Setting_Up_SRBs_for_Request_Sense"></span><span id="setting_up_srbs_for_request_sense"></span><span id="SETTING_UP_SRBS_FOR_REQUEST_SENSE"></span>设置请求检测 Srb

类驱动程序可以请求目标控制器返回检查条件时，端口驱动程序，返回的 SCSI 请求检测或等效身份信息。 若要执行此操作，在类驱动程序设置了**SenseInfoBuffer**指针和**SenseInfoBufferLength**在 SRB，因此端口驱动程序可以返回的请求检测信息如果检查条件。 端口驱动程序指示它通过设置返回请求检测信息**SrbStatus** SRB 成员\_状态\_自动感知\_返回 IRP 时有效。 有关详细信息*InterpretSenseInfo*例程，请参阅[存储类驱动程序 InterpretRequestSense 例程](storage-class-driver-s-interpretrequestsense-routine.md)。

### <a name="span-idretriesspanspan-idretriesspanspan-idretriesspanretries"></a><span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>重试次数

存储类驱动程序负责重试由于目标/控制器错误、 总线重置或请求超时而失败的请求。 因此，许多类驱动程序维护的 IRP 自己 I/O 堆栈位置中的重试计数。 这样的类驱动程序的*BuildRequest*例程还可能将初始化为给定请求的重试限制之前设置了其*IoCompletion*例程，并将 IRP 到端口驱动程序。 有关详细信息*RetryRequest*例程，请参阅[存储类驱动程序 RetryRequest 例程](storage-class-driver-s-retryrequest-routine.md)。

 

 




