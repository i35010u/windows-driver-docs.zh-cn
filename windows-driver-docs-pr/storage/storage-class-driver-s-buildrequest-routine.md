---
title: 存储类驱动程序的 BuildRequest 例程
description: 存储类驱动程序的 BuildRequest 例程
keywords:
- BuildRequest
- I/o 堆栈位置 WDK 存储
- 正在重试 WDK 存储
- SCSI 请求感知 WDK 存储
- 请求感知 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1962559e3fd1f5feb0c14a3d5677c32d9ea5fe7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837625"
---
# <a name="storage-class-drivers-buildrequest-routine"></a>存储类驱动程序的 BuildRequest 例程


## <span id="ddk_storage_class_drivers_buildrequest_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_BUILDREQUEST_ROUTINE_KG"></span>


与所有较高级别的内核模式驱动程序一样，存储类驱动程序必须在 [处理对存储外围设备的请求](handling-requests-to-storage-peripherals.md)时，为下一个较低版本的驱动程序设置 IRP 的 i/o 堆栈位置。 在类驱动程序为系统提供的端口驱动程序设置 SRBs 的 Irp 中，端口驱动程序的 i/o 堆栈位置设置如下：

-   **MajorFunction** 包含 IRP \_ MJ \_ SCSI

-   **Srb** 包含指向 Srb 的指针

每个类驱动程序负责为 SRBs 分配内存，以及通过 CDBs 为基础存储端口驱动程序设置内存。 类驱动程序可以为其具有 **ExInitializeNPageLookasideList** 的 SRBs 设置后备链表列表，或为非分页内存设置调用 **ExAllocatePool** 。 有关使用后备链表列表和非分页池的详细信息，请参阅 [使用后备链表列表](../kernel/using-lookaside-lists.md) 。

无论是从池分配内存，还是从驱动程序创建的后备链表列表分配内存，每个存储类驱动程序都将负责释放为 SRBs 分配的内存。 存储类驱动程序 [的 IoCompletion 例程](storage-class-driver-s-iocompletion-routines.md)中描述的存储类驱动程序 *IoCompletion* 例程通常将分配给 SRBs 的内存释放回后备链表列表。

类驱动程序的 *BuildRequest* 例程必须在 SRB 成员中设置适当的值，包括其设置为与其设备通信的 CDB 的长度。 对于返回请求感知信息和/或驱动程序可能需要重试的请求，它将在 IRP 中设置 *IoCompletion* 例程。 对于读取或写入请求，它会将 **SrbFlags** or 为适当的传输方向，并 \_ 分别 SRB 标记数据 \_ \_ 或 SRB \_ 标记 \_ 数据 \_ 。

*BuildRequest* 例程可能会分担使用一对 *SendSrbSynchronous* 和 *SendSrbAsynchronous* 例程设置 SRB 的责任。 也就是说， *BuildRequest* 例程可以设置通常为所有请求设置的 SRB 成员，而 *SendSrbXxx* 例程则每个设置的 SRB 值仅与每个请求类型相关。 将 IRP 从 *SendSrbAsynchronous* 例程向下传递到端口驱动程序时，必须使用驱动程序提供的 *IoCompletion* 例程来设置 irp。

加载类驱动程序后，它将设置大多数 SRBs，并将 **函数** 成员设置为 SRB \_ function \_ EXECUTE \_ SCSI，指示要通过总线发送的设备 i/o 请求。

有关系统定义的 SRB 成员及其值的详细信息，请参阅 [**SCSI \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)。

### <a name="span-idsetting_up_srbs_for_request_sensespanspan-idsetting_up_srbs_for_request_sensespanspan-idsetting_up_srbs_for_request_sensespansetting-up-srbs-for-request-sense"></a><span id="Setting_Up_SRBs_for_Request_Sense"></span><span id="setting_up_srbs_for_request_sense"></span><span id="SETTING_UP_SRBS_FOR_REQUEST_SENSE"></span>为请求感知设置 SRBs

类驱动程序可以请求端口驱动程序在目标控制器返回检查条件时返回 SCSI 请求感知或等效信息。 为此，类驱动程序会在 SRB 中设置 **SenseInfoBuffer** 指针和 **SenseInfoBufferLength** ，以便在出现检查条件时，端口驱动程序可以返回请求感知信息。 端口驱动程序指示它通过 **SrbStatus** \_ \_ \_ 在返回 IRP 时通过将 SrbStatus 成员设置为 SRB 状态自动感知来返回请求感知信息。 有关 *InterpretSenseInfo* 例程的详细信息，请参阅 [存储类驱动程序的 InterpretRequestSense 例程](storage-class-driver-s-interpretrequestsense-routine.md)。

### <a name="span-idretriesspanspan-idretriesspanspan-idretriesspanretries"></a><span id="Retries"></span><span id="retries"></span><span id="RETRIES"></span>重试

存储类驱动程序负责重试因目标/控制器错误、总线重置或请求超时而失败的请求。 因此，许多类驱动程序在 IRP 的 i/o 堆栈位置中保留重试计数。 此类驱动程序的 *BuildRequest* 例程还可以在设置其 *IoCompletion* 例程并将 IRP 发送到端口驱动程序之前，初始化给定请求的重试限制。 有关 *RetryRequest* 例程的详细信息，请参阅 [存储类驱动程序的 RetryRequest 例程](storage-class-driver-s-retryrequest-routine.md)。

 

