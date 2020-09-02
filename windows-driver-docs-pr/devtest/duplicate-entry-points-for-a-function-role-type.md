---
title: 函数角色类型的重复入口点
description: 函数角色类型的重复入口点
ms.assetid: cf6604da-bd79-4adf-a08f-9b903aa91133
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e20a22056bda72fc8d2d97e6f79cc6d5a82c66f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383257"
---
# <a name="duplicate-entry-points-for-a-function-role-type"></a>函数角色类型的重复入口点


对于大多数函数角色类型，SDV 假定驱动程序的每个入口点最多只有一个回调函数。 但是，有一些函数角色类型可以有多个与之关联的事件回调函数。 例如，KMDF 驱动程序可能会有多个 [*EvtTimerFunc*](/windows-hardware/drivers/ddi/wdftimer/nc-wdftimer-evt_wdf_timer) 或 [*EvtDpcFunc*](/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) 回调函数 (这些函数使用 .evt \_ wdf \_ 计时器，并 \_ \_)  在这种情况下，SDV 会将一个整数追加到 Sdv 中的函数类型。 例如，如果你的驱动程序有两个 DPC 回叫函数，SDV 会将它们映射到 **有趣的 \_ wdf \_ dpc \_ 1** 和 **有趣的 \_ wdf \_ dpc \_ 2**。

如果驱动程序超过了某个角色类型的最大回调函数数，SDV 将显示以下消息。

```
Static Driver Verifier found more than one entry point for '[role type]'
```

如果函数角色类型具有比 SDV 支持的更多的入口点，则驱动程序不一定有问题。 但是，若要获得准确的验证结果，必须编辑 Sdv 文件以删除重复的项。

例如，下面的 Sdv 文件显示有两个 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 函数，它们是使用 ".Evt \_ WDF \_ 请求 \_ 完成" \_ 例程角色类型进行批注的。 在 Sdv 文件中，SDV 将 **EvtRequestReadCompletionRoutine** 和 **EvtRequestWriteCompletionRoutine** 定义为有趣的 \_ WDF \_ 请求 \_ 完成 \_ 例程。

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

若要删除重复项，请将第二个完成例程注释掉 (将定义中的** \# d**替换 \# 为两个注释分隔符 (**//**) "。 然后，将 " **已批准** " 设置为 "true" 并运行验证。

```
#define fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestReadCompletionRoutine
//efine fun_WDF_REQUEST_COMPLETION_ROUTINE EvtRequestWriteCompletionRoutine
```

使用一个完成例程查看验证结果后，请再次编辑 Sdv 文件，但这一次，注释掉刚刚验证的完成例程并删除注释， (将替换 **//** 例程中的 with ** \# d**) 替换为未验证。 然后再次运行 SDV。

### <a name="span-idfunction_role_types_that_support_multiple_entry_pointsspanspan-idfunction_role_types_that_support_multiple_entry_pointsspanfunction-role-types-that-support-multiple-entry-points"></a><span id="function_role_types_that_support_multiple_entry_points"></span><span id="FUNCTION_ROLE_TYPES_THAT_SUPPORT_MULTIPLE_ENTRY_POINTS"></span>支持多个入口点的函数角色类型

某些函数角色类型支持多个条目。 如果条目数超过了支持的最大值，则 SDV 还会将其报告为重复项。 可以通过在 Sdv 文件中选择性地注释掉回调例程的** \# define**语句并进行单独的验证来处理这些附加条目，这与处理重复项的方式相同。 例如，如果你的驱动程序具有八个使用 .EVT \_ WDF \_ dpc role type)  (，则可以执行以下操作：

-   编辑 Sdv，并注释掉有趣的 \_ wdf dpc \_ \_ 5 到有趣的 \_ wdf \_ dpc \_ 8 的定义语句。

-   在驱动程序上运行 SDV。

-   然后再次编辑 Sdv，以定义有趣的 wdf dpc \_ \_ \_ 5 到有趣的 \_ wdf \_ dpc \_ 8，并注释掉有趣的 wdf dpc \_ \_ \_ 1 到有趣的 \_ wdf \_ dpc \_ 4 的定义语句。

-   在驱动程序上运行 SDV。

有关可包含多个回调函数的函数角色类型的列表，请参阅 [Static Driver VERIFIER KMDF 批注](static-driver-verifier-kmdf-function-declarations.md) 。 此列表显示 SDV 为这些角色类型支持的回调函数的最大数目。

 

