---
title: 函数角色类型的重复入口点
description: 函数角色类型的重复入口点
ms.assetid: cf6604da-bd79-4adf-a08f-9b903aa91133
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e15e875670d67fe62ba60fab1c71ceaca52bc536
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371501"
---
# <a name="duplicate-entry-points-for-a-function-role-type"></a>函数角色类型的重复入口点


对于大多数函数角色类型，SDV 假设驱动程序，最多为每个入口点的一个回调函数。 但是，有一些函数角色类型可以具有多个与之关联的事件回调函数。 例如，KMDF 驱动程序可能有多个[ *EvtTimerFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nc-wdftimer-evt_wdf_timer)或[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc) （使用 EVT的回调函数\_WDF\_计时器和 EVT\_WDF\_DPC 角色类型批注)。 在这种情况下，SDV 将追加到 Sdv map.h 中的函数类型的整数。 例如，如果您的驱动程序有两个 DPC 回调函数，SDV 将它们映射到**有趣\_WDF\_DPC\_1**并**有趣\_WDF\_DPC\_2**.

如果驱动程序超过了角色类型的回调函数的最大数目，SDV 显示以下消息。

```
Static Driver Verifier found more than one entry point for '[role type]'
```

如果函数角色类型具有多个入口点不是 SDV 支持，不一定存在驱动程序出现了一些问题。 但是，若要获取正确的验证结果，则必须编辑 Sdv。-map.h 文件以删除重复项。

例如，下面的 Sdv map.h 文件显示有两个[ *CompletionRoutine* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)函数进行批注使用 EVT\_WDF\_请求\_完成\_例程角色类型。 在 Sdv map.h 文件中，SDV 同时定义**EvtRequestReadCompletionRoutine**并**EvtRequestWriteCompletionRoutine**那么有趣了\_WDF\_请求\_完成\_例程。

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

若要删除重复项，注释掉第二个完成例程 (替换 **\#d**中\#定义具有两个注释分隔符 ( **//** )。 然后设置**Approved = true**并运行验证。

```
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestReadCompletionRoutine
//efine fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestWriteCompletionRoutine
```

查看过的一个完成例程与验证结果后，再次，编辑 Sdv map.h 文件，但此时间注释只验证完成例程并删除注释 (替换 **//** 与 **\#d**) 从没有经过验证完成例程。 然后再次运行 SDV。

### <a name="span-idfunctionroletypesthatsupportmultipleentrypointsspanspan-idfunctionroletypesthatsupportmultipleentrypointsspanfunction-role-types-that-support-multiple-entry-points"></a><span id="function_role_types_that_support_multiple_entry_points"></span><span id="FUNCTION_ROLE_TYPES_THAT_SUPPORT_MULTIPLE_ENTRY_POINTS"></span>函数支持多个入口点的角色类型

某些函数角色类型支持多个条目。 如果条目数超过了支持的最大，SDV 还报告它们作为重复项。 您可以将这些其他项的一样来处理重复项，有选择地注释掉 **\#定义**语句中的 Sdv map.h 文件也使单独的回调例程验证。 例如，如果您的驱动程序具有八个 DPC 回调函数 (使用 EVT\_WDF\_DPC 角色类型)，则可以执行以下操作：

-   编辑 Sdv map.h 并注释掉定义语句为了增添些乐趣\_WDF\_DPC\_5 至有趣\_WDF\_DPC\_8。

-   该驱动程序上再次运行 SDV。

-   然后，编辑 Sdv-map.h 再次来定义有趣\_WDF\_DPC\_5 至有趣\_WDF\_DPC\_8 并注释掉定义语句为了增添些乐趣\_WDF\_DPC\_1 到有趣\_WDF\_DPC\_4。

-   该驱动程序上再次运行 SDV。

请参阅[静态驱动程序验证工具 KMDF 批注](static-driver-verifier-kmdf-function-declarations.md)有关函数角色类型可以具有多个回调函数的列表。 列表显示 SDV 支持这些角色类型的回调函数的最大数目。

 

 





