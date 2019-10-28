---
title: 函数角色类型的重复入口点
description: 函数角色类型的重复入口点
ms.assetid: cf6604da-bd79-4adf-a08f-9b903aa91133
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 392d542012d83396223c12909089f4d510298577
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839562"
---
# <a name="duplicate-entry-points-for-a-function-role-type"></a>函数角色类型的重复入口点


对于大多数函数角色类型，SDV 假定驱动程序的每个入口点最多只有一个回调函数。 但是，有一些函数角色类型可以有多个与之关联的事件回调函数。 例如，KMDF 驱动程序可能有多个[*EvtTimerFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer)或[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回叫函数（使用 .EVT\_wdf\_TIMER 和\_.evt\_DPC 角色类型注释）。 在这种情况下，SDV 会将一个整数追加到 Sdv 中的函数类型。 例如，如果你的驱动程序有两个 DPC 回叫函数，SDV 会将它们映射到**有趣的\_wdf\_dpc\_1** ，**有趣的\_WDF\_dpc\_2**。

如果驱动程序超过了某个角色类型的最大回调函数数，SDV 将显示以下消息。

```
Static Driver Verifier found more than one entry point for '[role type]'
```

如果函数角色类型具有比 SDV 支持的更多的入口点，则驱动程序不一定有问题。 但是，若要获得准确的验证结果，必须编辑 Sdv 文件以删除重复的项。

例如，下面的 Sdv 文件显示有两个[*CompletionRoutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)函数，它们使用 .EVT\_WDF\_请求\_完成\_常规角色类型。 在 Sdv 文件中，SDV 将**EvtRequestReadCompletionRoutine**和**EvtRequestWriteCompletionRoutine**定义为有趣\_WDF\_请求\_完成\_例程。

```
//Approved=false
#define fun_WDF_DRIVER_DEVICE_ADD OsrFxEvtDeviceAdd
#define fun_WDF_IO_QUEUE_IO_READ OsrFxEvtIoRead
#define fun_WDF_IO_QUEUE_IO_STOP OsrFxEvtIoStop
#define fun_WDF_DEVICE_D0_EXIT OsrFxEvtDeviceD0Exit
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestReadCompletionRoutine
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestWriteCompletionRoutine
#define fun_WDF_OBJECT_CONTEXT_CLEANUP OsrFxEvtDriverContextCleanup
#define fun_WDF_DEVICE_D0_ENTRY OsrFxEvtDeviceD0Entry
#define fun_WDF_DEVICE_PREPARE_HARDWARE OsrFxEvtDevicePrepareHardware
#define fun_WDF_IO_QUEUE_IO_WRITE OsrFxEvtIoWrite
#define fun_WDF_IO_QUEUE_IO_DEVICE_CONTROL OsrFxEvtIoDeviceControl
```

若要删除重复项，请将第二个完成例程注释掉（将 \#定义中的 **\#d**替换为两个注释分隔符（ **//** ）。 然后，将 "**已批准**" 设置为 "true" 并运行验证。

```
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestReadCompletionRoutine
//efine fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestWriteCompletionRoutine
```

使用一个完成例程查看验证结果后，请再次编辑 Sdv 文件，但这一次会注释掉刚刚验证的完成例程，并删除注释（将 **//** 替换为 **\#d**）进行验证。 然后再次运行 SDV。

### <a name="span-idfunction_role_types_that_support_multiple_entry_pointsspanspan-idfunction_role_types_that_support_multiple_entry_pointsspanfunction-role-types-that-support-multiple-entry-points"></a><span id="function_role_types_that_support_multiple_entry_points"></span><span id="FUNCTION_ROLE_TYPES_THAT_SUPPORT_MULTIPLE_ENTRY_POINTS"></span>支持多个入口点的函数角色类型

某些函数角色类型支持多个条目。 如果条目数超过了支持的最大值，则 SDV 还会将其报告为重复项。 您可以使用与处理重复项相同的方式来处理这些附加项，方法是有选择性地注释\#掉 Sdv 文件中的回调例程的**定义**语句，并进行单独的验证。 例如，如果你的驱动程序有8个 DPC 回叫函数（使用 .EVT\_WDF\_DPC 角色类型），则可以执行以下操作：

-   编辑 Sdv，并注释掉用于趣味\_WDF 的 define 语句\_DPC\_5 到\_趣味\_DPC\_8。

-   在驱动程序上运行 SDV。

-   然后再次编辑 Sdv，以定义趣味\_WDF\_DPC\_5 到\_趣味\_DPC\_，并注释掉有趣的 define 语句\_DPC\_\_WDF\_DPC\_4。

-   在驱动程序上运行 SDV。

有关可包含多个回调函数的函数角色类型的列表，请参阅[Static Driver VERIFIER KMDF 批注](static-driver-verifier-kmdf-function-declarations.md)。 此列表显示 SDV 为这些角色类型支持的回调函数的最大数目。

 

 





