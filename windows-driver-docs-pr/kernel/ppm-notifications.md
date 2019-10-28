---
title: 处理器电源管理 (PPM) 通知
description: PEP 的 AcceptProcessorNotification 回调例程收到的每个处理器电源管理（PPM）通知都附带了通知参数，该参数指示通知的类型，以及指向数据结构的数据参数。包含指定通知类型信息的。
ms.assetid: 4BA89D0F-78F0-44DF-BC9B-0F9F3256CD59
keywords:
- AcceptProcessorNotification 回调
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1d2ccfc2fd1da5950a0162148f864f5607e2c6b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838496"
---
# <a name="processor-power-management-ppm-notifications"></a>处理器电源管理 (PPM) 通知

PEP 的[*AcceptProcessorNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifyppm)回调例程收到的每个处理器电源管理（PPM）通知都附带了通知参数，该参数指示通知的类型，以及指向数据的数据参数包含指定通知类型信息的结构。

在此调用中，通知参数设置为指示通知类型的 PEP_NOTIFY_PPM_XXX 常量值。 数据参数指向与此通知类型相关联的 PEP_PPM_XXX 结构类型。

AcceptProcessorNotification 回调例程使用以下处理器电源管理（PPM）通知 Id。

## <a name="pep_notify_ppm_query_capabilities"></a>PEP_NOTIFY_PPM_QUERY_CAPABILITIES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_CAPABILITIES。

*数据*

指向 PEP_PPM_QUERY_CAPABILITIES 结构的指针。

**备注**

通知 PEP 正在查询它以获取 PEP 的电源管理功能。

当查询 PEP 的电源管理功能时，Windows 电源管理框架（PoFx）将发送此通知。 这会在处理器初始化时出现，并将发送给系统中的每个处理器。

具有 x86/AMD64 处理器的平台必须使用 ACPI 接口进行处理器性能控制。

若要发送 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知，PoFx 将调用 PEP 的 AcceptProcessorNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_PPM_QUERY_CAPABILITIES，Data 参数指向 PEP_PPM_QUERY_CAPABILITIES 结构。

对于 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

 
## <a name="pep_notify_ppm_query_idle_states"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES 

*通知*

值 PEP_NOTIFY_PPM_QUERY_IDLE_STATES。

*数据*

指向 PEP_PPM_QUERY_IDLE_STATES 结构的指针。

**备注**

通知 PEP 有关空闲状态的信息。

若要发送 PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知，PoFx 将调用 PEP 的 AcceptProcessorNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_PPM_QUERY_IDLE_STATES，Data 参数指向 PEP_PPM_QUERY_IDLE_STATES 结构。

对于 PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

 
## <a name="pep_notify_ppm_idle_select"></a>PEP_NOTIFY_PPM_IDLE_SELECT 

*通知*

值 PEP_NOTIFY_PPM_IDLE_SELECT。

*数据*

指向 PEP_PPM_IDLE_SELECT 结构的指针。

**备注**

向 PEP 通知 "空闲" 选择。

若要发送 PEP_NOTIFY_PPM_IDLE_SELECT 通知，PoFx 将调用 PEP 的 AcceptProcessorNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_PPM_IDLE_SELECT，Data 参数指向 PEP_PPM_IDLE_SELECT 结构。

对于 PEP_NOTIFY_PPM_IDLE_SELECT 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_idle_cancel"></a>PEP_NOTIFY_PPM_IDLE_CANCEL 

*通知*

值 PEP_NOTIFY_PPM_IDLE_CANCEL。

*数据*

指向 PEP_PPM_IDLE_CANCEL 结构的指针。

**备注**

通知 PEP 取消操作。

若要发送 PEP_NOTIFY_PPM_IDLE_CANCEL 通知，PoFx 将调用 PEP 的 AcceptProcessorNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_PPM_IDLE_CANCEL，Data 参数指向 PEP_PPM_IDLE_CANCEL 结构。

对于 PEP_NOTIFY_PPM_IDLE_CANCEL 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。

 
## <a name="pep_notify_ppm_idle_execute"></a>PEP_NOTIFY_PPM_IDLE_EXECUTE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_IDLE_EXECUTE。

*数据*

指向 PEP_PPM_IDLE_EXECUTE 或 PEP_PPM_IDLE_EXECUTE_V2 结构的指针。

**备注**

发送到 PEP，以将当前处理器转换为指定的空闲状态。

Windows 电源管理框架（PoFx）将此通知发送到 PEP，以将当前处理器转换为指定的空闲状态。 

PEP 可以准备硬件来进入之前选择的空闲状态，包括通知核心系统资源的操作系统，这些资源可能受睡眠转换的影响。 然后，必须执行停止指令以将处理器转换为空闲状态。 从空闲状态返回后，PEP 必须撤消硬件设置，包括通知核心系统资源的操作系统，这些资源可能在唤醒时变为活动状态。 如果 PEP 无法执行处理器（和平台）空闲状态，则必须返回错误状态。

使用协调式空闲状态接口时，操作系统使用 PEP_PPM_IDLE_EXECUTE_V2 结构，其中包括 CoordinatedStateCount 和 CoordinatedState 字段以及空闲转换将输入的协调空闲状态的列表。 PlatformState 字段将指定所输入的最深层的平台协调空闲状态（如果有）。 

当不使用协调式空闲状态接口时，操作系统将使用 PEP_PPM_IDLE_EXECUTE 结构。 

对于 PEP_NOTIFY_PPM_IDLE_EXECUTE 通知，会调用 AcceptProcessorNotification 例程并禁用中断。
 
## <a name="pep_notify_ppm_idle_complete"></a>PEP_NOTIFY_PPM_IDLE_COMPLETE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 

*通知*

值 PEP_NOTIFY_PPM_IDLE_COMPLETE。

*数据*

指向 PEP_PPM_IDLE_COMPLETE 或 PEP_PPM_IDLE_COMPLETE_V2 结构的指针。

**备注**

通知 PEP 当前处理器正在从完成的空闲转换中唤醒。

当当前处理器从已完成的空闲转换中唤醒时，Windows 电源管理框架（PoFx）将发送此通知。 如果平台执行的是平台空闲转换，则第一个唤醒的处理器将指示正在退出的平台空闲状态。 根据平台空闲转换中使用的同步类型，第一个从平台空闲状态唤醒的处理器可能不是进入平台空闲状态的处理器。 

如果处理器执行的是深度空闲状态，则 PEP 不得等待，直到收到用于还原核心上下文的完整通知或通知操作系统已还原核心资源。 执行通知完成后，操作系统将会恢复这些资源。 启用虚拟机监控程序后，PEP 仅在退出平台空闲状态时才会收到此通知，并且 ProcessorState 字段设置为 PEP_PROCESSOR_IDLE_STATE_UNKNOWN。 

使用协调式空闲状态接口时，操作系统使用 PEP_PPM_IDLE_COMPLETE_V2 结构，其中包括 CoordinatedStateCount 和 CoordinatedState 字段以及空闲转换将退出的协调空闲状态的列表。 PlatformState 字段将指定即将退出的最深层平台协调空闲状态（如果有）。 请注意，如果使用松散同步，则此处理器退出的协调空闲状态集可能不同于它输入的协调空闲状态集。 

当不使用协调式空闲状态接口时，操作系统将使用 PEP_PPM_IDLE_COMPLETE 结构。 

对于 PEP_NOTIFY_PPM_IDLE_COMPLETE 通知，会调用 AcceptProcessorNotification 例程并禁用中断，并且始终在目标处理器上执行。
 
## <a name="pep_notify_ppm_is_processor_halted"></a>PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED。

*数据*

指向 PEP_PPM_IS_PROCESSOR_HALTED 结构的指针。

**备注**

发送到 PEP，确定指定的处理器当前是否在其所选的空闲状态中暂停。

Windows 电源管理框架（PoFx）会将此通知发送到 PEP，以确定指定的处理器当前是否在其所选的空闲状态下停止。 当协调平台空闲状态时，操作系统将使用此通知来检查辅助处理器是否已完全完成过渡到空闲状态。 PEP 必须保证目标处理器已达到平台空闲转换可安全发生的状态（例如，通过检查硬件寄存器来查看核心是否已停止）。 此通知指示处理器处于空闲状态后，该处理器必须不会唤醒，除非操作系统显式请求它这样做。 

此 PEP 可能会在 IDLE_SELECT 和 IDLE_COMPLETE 通知之间随时收到此通知。 保证在空闲转换期间最多接收一次此通知。 

对于 PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 通知，AcceptProcessorNotification 例程将在任何 IRQL 处调用，禁用中断，任何 IRQL，且永远不会在目标处理器上执行。

< = HIGH_LEVEL
 
## <a name="pep_notify_ppm_initiate_wake"></a>PEP_NOTIFY_PPM_INITIATE_WAKE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。

*通知*

值 PEP_NOTIFY_PPM_INITIATE_WAKE。

*数据*

指向结构的指针。

**备注**

发送到特定处理器的 PEP，以从不可中断的空闲状态唤醒。

Windows 电源管理框架（PoFx）将此通知发送到指定处理器的 PEP，以从不可中断的空闲状态唤醒。 PEP 必须使用 NeedInterruptForCompletion 返回目标处理器的唤醒状态。 如果处理器需要中断来完成从空闲状态唤醒，则返回 TRUE。 在这种情况下，PEP 必须确保在从处理此通知返回后中断目标处理器。 如果目标处理器已在运行，并且/或者最终将退出空闲状态（在执行此操作的过程中），则不需要任何软件产生中断，NeedInterruptForCompletion 应设置为 FALSE。


请注意，PEP 不会同时在同一处理器上收到此通知。
 

对于 PEP_NOTIFY_PPM_INITIATE_WAKE 通知，AcceptProcessorNotification 例程在任何 IRQL 上调用，禁用中断，并且永远不会在目标处理器上执行。

< = HIGH_LEVEL
 
## <a name="pep_notify_ppm_query_feedback_counters"></a>PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS。

*数据*

指向 PEP_PPM_QUERY_FEEDBACK_COUNTERS 结构的指针。

**备注**

告知 PEP 正在查询它所支持的反馈计数器列表。

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以便在 PEP 中查询它所支持的反馈计数器列表。

对于 PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_feedback_read"></a>PEP_NOTIFY_PPM_FEEDBACK_READ 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_FEEDBACK_READ。

*数据*

指向 PEP_PPM_FEEDBACK_READ 结构的指针。

**备注**

通知 PEP 正在查询其反馈计数器的当前值。

当 Windows 电源管理框架（PoFx）要查询反馈计数器的当前值时，将发送此通知。 

禁用中断后，可能会发送此通知。 如果已设置计数器的关联字段，则会在目标处理器上执行此通知。 否则，可能会从任何处理器执行此通知。

对于 PEP_NOTIFY_PPM_FEEDBACK_READ 通知，可以在 IRQL = DISPATCH_LEVEL 调用 AcceptProcessorNotification 例程。

 
## <a name="pep_notify_ppm_query_perf_capabilities"></a>PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES。

*数据*

指向 PEP_PPM_QUERY_PERF_CAPABILITIES 结构的指针。

**备注**

通知 PEP 正在查询该平台支持的性能范围。

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以查询该平台支持的性能范围。 PEP_PPM_QUERY_PERF_CAPABILITIES 结构的 DomainId 和 DomainMembers 字段用于将性能状态域表达到平台。 每个处理器只是一个性能状态域的成员。 操作系统将确保性能域中的所有处理器都同时更改性能。 

对于 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_perf_constraints"></a>PEP_NOTIFY_PPM_PERF_CONSTRAINTS 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 

*通知*

值 PEP_NOTIFY_PPM_PERF_CONSTRAINTS。

*数据*

指向 PEP_PPM_PERF_CONSTRAINTS 结构的指针。

**备注**

通知 PEP 要查询处理器当前操作约束的情况。

当 Windows 电源管理框架（PoFx）要检查处理器当前的操作约束时，将发送此通知。 PEP 通过执行控制代码 GUID_PPM_PERF_CONSTRAINT_CHANGE 的电源控制来启动操作系统请求，以重新评估处理器的 perf 限制。 InBuffer 和 OutBuffer 必须为 NULL。 

在为处理器发出电源控制事务之前，PEP 必须等待，直到它收到 PEP_DPM_DEVICE_STARTED 通知。 

对于 PEP_NOTIFY_PPM_PERF_CONSTRAINTS 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_perf_set"></a>PEP_NOTIFY_PPM_PERF_SET 
 
此通知告知 PEP 应更改处理器的当前操作性能。

以下描述了[*AcceptProcessorNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifyppm)的参数。

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值**PEP_NOTIFY_PPM_PERF_SET**。

*数据*

指向[**PEP_PPM_PERF_SET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/pep_x/ns-pep_x-_pep_ppm_perf_set)结构的指针。

**备注**

当 Windows 电源管理框架（PoFx）要更改处理器的当前运行性能时，会发送此通知。 在任何处理器上执行时，可能会发送此通知。

对于 PEP_NOTIFY_PPM_PERF_SET 通知， *AcceptProcessorNotification*例程始终调用 IRQL = DISPATCH_LEVEL。

 
## <a name="pep_notify_ppm_park_selection"></a>PEP_NOTIFY_PPM_PARK_SELECTION 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_PARK_SELECTION。

*数据*

指向 PEP_PPM_PARK_SELECTION 结构的指针。

**备注**

通知 PEP，操作系统希望它选择一个要驻留的首选处理器核心集。

Windows 电源管理框架（PoFx）发送此通知以指示 PEP 选择要驻留的首选核心集。

PEP_NOTIFY_PPM_PARK_SELECTION 已重载以执行两个功能： 

让 PEP 从系统中的所有处理器集内选择哪些处理器应被暂停，哪些处理器应被放置。 让 PEP 从已离开的所有处理器的集中选择哪些处理器应接收中断，而不应接收中断。 Windows 不会为 PEP 提供一种方式来区分 OS 正在执行哪两个目标。 因此，当 PEP 接收到带有一组给定输入（AdditionalUnparkedProcessors 计数和 PoPreference）的通知时，它应提供一致的输出（PepPreference），除非某个外部事件导致 PEP 首选项发生更改。 

对于 PEP_NOTIFY_PPM_PARK_SELECTION 通知，AcceptProcessorNotification 例程始终调用 IRQL = DISPATCH_LEVEL。

 
## <a name="pep_notify_ppm_cst_states"></a>PEP_NOTIFY_PPM_CST_STATES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_CST_STATES。

*数据*

指向 PEP_PPM_CST_STATES 结构的指针。

**备注**

发送到 PEP，指示处理器支持的一系列 ACPI 定义的 C 状态。 

Windows 电源管理框架（PoFx）会将此通知发送到 PEP，以指示处理器支持的一系列 ACPI 定义的 C 状态。 此通知将在第一次第一次使用 PEP 接收到处理器的 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知之前发送一次，并在处理器收到指示 _CST 对象已更改的通知（0x81）时再次发送。

对于 PEP_NOTIFY_PPM_CST_STATES 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_platform_states"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES。

*数据*

指向 PEP_PPM_QUERY_PLATFORM_STATES 结构的指针。

**备注**

在处理器初始化时发送，用于查询 PEP 支持的平台空闲状态数。

Windows 电源管理框架（PoFx）会将此通知发送到 PEP 的处理器初始化，以查询它支持的平台空闲状态的数目。 此通知将在启动后立即发送。 返回非零的平台状态后，PEP 可以在处理器空闲转换期间开始选择平台空闲状态。

对于 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_lp_settings"></a>PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 

*通知*

值 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS。

*数据*

指向 PEP_PPM_QUERY_LP_SETTINGS 结构的指针。

**备注**

 若要发送 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知，PoFx 将调用 PEP 的 AcceptProcessorNotification 回调例程。 在此调用中，通知参数值为 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS，Data 参数指向 PEP_PPM_QUERY_LP_SETTINGS 结构。

对于 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_idle_states_v2"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2。

*数据*

指向 PEP_PPM_QUERY_IDLE_STATES_V2 结构的指针。

**备注**

 在处理器初始化中用于查询 PEP 支持的空闲状态的列表。

Windows 电源管理框架（PoFx）将此通知发送到 PEP 的处理器初始化，以查询它支持的空闲状态的列表。 

Count 成员指定空闲状态数组的大小。 在发送此通知之前，处理器驱动程序将查询具有 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 的空闲状态的数目。 

PEP 会在 IdleStates 阵列中填充它所支持的每个空闲状态的相关信息。 应按照降低功率消耗/增加转换成本的顺序列出空闲状态。 不需要 PEP 报告每个处理器的相同空闲状态列表。 

对于 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_platform_state"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE。

*数据*

指向 PEP_PPM_QUERY_PLATFORM_STATE 结构的指针。

**备注**

发送到 PEP 以查询单个平台空闲状态的属性。

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以查询单个平台空闲状态的属性。 

PEP_PPM_QUERY_PLATFORM_STATE 结构的 StateIndex 参数指定正在查询的平台空闲状态的索引。 在发送此通知之前，处理器驱动程序将查询具有 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 的受支持平台空闲状态的数目。 然后，处理器驱动程序将为每个平台空闲状态发送一个 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知。 在所有处理器都注册到 PEP 之前，处理器驱动程序将等待发送此通知。 

PEP 用有关平台空闲状态的信息填充状态结构。 平台空闲状态应按照降低功率消耗/增加转换成本的顺序列出。 

对于 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_test_idle_state"></a>PEP_NOTIFY_PPM_TEST_IDLE_STATE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_TEST_IDLE_STATE。

*数据*

指向 PEP_PPM_TEST_IDLE_STATE 结构的指针。

**备注**

 用于测试是否可以在指定处理器上输入指定的处理器和平台空闲状态。

Windows 电源管理框架（PoFx）发送此通知，以测试是否可以在指定的处理器上输入指定的处理器和平台空闲状态。 如果可以进入空闲状态，则 PEP 会在否决代码 PEP_IDLE_VETO_NONE 中填入并完成空闲转换。 如果由于某种原因无法完成空闲转换，PEP 将填充非零的拒绝代码。 

介于0x80000000 到0xffffffff 范围内的重要否决代码是为 OS 使用而保留的，不能使用。
 

发送此通知时，操作系统已验证与所选处理器或平台空闲状态关联的所有约束是否均已满足，包括平台空闲转换的设备和处理器约束。 

此通知将在操作系统尝试进入任何处理器或平台空闲状态之前发送，但带有索引0的处理器空闲状态除外，该状态必须始终为 enterable。 用 PEP_IDLE_VETO_NONE 完成此通知并不保证 OS 将进入指示的空闲状态。 禁用中断后发送此通知。 此通知始终在目标处理器上执行。 

对于 PEP_NOTIFY_PPM_TEST_IDLE_STATE 通知，会调用 AcceptProcessorNotification 例程并禁用中断。
 
## <a name="pep_notify_ppm_idle_pre_execute"></a>PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE。

*数据*

指向 PEP_PPM_IDLE_EXECUTE 或 PEP_PPM_IDLE_EXECUTE_V2 结构的指针。

**备注**

发送到 PEP，使系统能够转换到指定的空闲状态。

Windows 电源管理框架（PoFx）将此通知发送到 PEP，使系统能够转换到指定的空闲状态。 成功完成此通知后，操作系统会通过输入关联的 C 状态将处理器转换为空闲状态。 如果 PEP 无法准备系统来进入处理器（和平台）空闲状态，则必须返回错误状态。 

当启用虚拟机监控程序时，PEP 仅在进入平台空闲状态时才会收到此通知，并且 ProcessorState 字段设置为 PEP_PROCESSOR_IDLE_STATE_UNKNOWN。 

使用协调式空闲状态接口时，操作系统使用 PEP_PPM_IDLE_EXECUTE_V2 结构，其中包括 CoordinatedStateCount 和 CoordinatedState 字段以及空闲转换将输入的协调空闲状态的列表。 PlatformState 字段将指定所输入的最深层的平台协调空闲状态（如果有）。 

当不使用协调式空闲状态接口时，操作系统将使用 PEP_PPM_IDLE_EXECUTE 结构。 

对于 PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 通知，会调用 AcceptProcessorNotification 例程并禁用中断，并且始终在目标处理器上执行。
 
## <a name="pep_notify_ppm_update_platform_state"></a>PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE。

*数据*

指向 PEP_PPM_QUERY_PLATFORM_STATE 结构的指针。

**备注**

通知 PEP 处理器已收到通知（0x81），用于更新平台空闲状态的特征。

当处理器收到通知（0x81）来更新平台空闲状态的特征时，Windows 电源管理框架（PoFx）将发送此通知。 对于每个平台空闲状态一次发送此通知。 如果 PEP 不接受通知（即从其 AcceptProcessorNotification 回调返回 FALSE），则为先前的平台空闲状态定义（从最近接受的 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 或 PEP_NOTIFY_PPM_）。保留 UPDATE_PLATFORM_STATE 通知。 

此通知使用与 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知相同的数据缓冲区。 

对于 PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_platform_state_residencies"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES。

*数据*

指向 PEP_PPM_PLATFORM_STATE_RESIDENCIES 结构的指针。

**备注**

通知 PEP 应该捕获自启动后每个平台空闲状态所用的实际累计时间。

Windows 电源管理框架（PoFx）会将此通知发送到 PEP，以捕获自启动后每个平台空闲状态所用的实际累计时间。 因此，此查询仅适用于基础硬件可能自主决定进入不同于操作系统所请求的平台空闲状态的平台。 返回的值用于诊断目的，确定平台空闲状态派驻操作系统的视图与平台实际实现的不同之处。 

Count 指定状态数组中的元素数，其中，元素索引对应于平台空闲状态索引。 PEP 将用匹配状态的实际驻留和转换计数填充每个元素。 


请注意，此查询捕获的累计值应该只对应于 PEP （或处理器驱动程序）实际执行了平台空闲状态转换的那段时间。 这将确保 OS 计算的常驻与实际派驻服务之间的比较有意义。
 

对于 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 通知，可以在任何 IRQL 上调用 AcceptProcessorNotification 例程。
 
## <a name="pep_notify_ppm_query_veto_reasons"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASONS 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_VETO_REASONS。

*数据*

指向 PEP_PPM_QUERY_VETO_REASONS 结构的指针。

**备注**

 用于查询 PEP 在 ProcessorIdleVeto 和 PlatformIdleVeto 回调中使用的独特否决原因的数目。 

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以查询 PEP 在 ProcessorIdleVeto 和 PlatformIdleVeto 回调中使用的独特否决原因的数目。 此通知是可选的，它可能会被 PEP 忽略。 

如果接受，则允许 PEP 使用介于1和 VetoReasonCount （含）之间的拒绝原因来否决任何处理器、平台或协调的空闲状态。 不允许使用超过 VetoReasonCount 的拒绝原因。 操作系统将预分配拒绝跟踪结构，与 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 一起使用时，保证所有处理器、平台和协调状态否决回调都将成功。

如果 PEP 未接受此通知，PEP 可能会出于法律拒绝原因使用 ProcessorIdleVeto 和 PlatformIdleVeto 回调。 操作系统不保证回调会因为分配失败或其他问题而失败。

对于 PEP_NOTIFY_PPM_QUERY_VETO_REASONS 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_veto_reason"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASON 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_VETO_REASON。

*数据*

指向 PEP_PPM_QUERY_VETO_REASON 结构的指针。

**备注**

发送到 PEP 以查询特定否决原因的相关信息。

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以查询有关特定否决原因的信息。 对于每个否决原因，此通知将发送两次，一次使用 NULLName 的缓冲区来检索名称所需的分配大小，使用非 NULLName 缓冲区填充名称的内容。 该名称应为可读的字符串，指示此否决原因所代表的条件。 当诊断不输入空闲状态的原因时，调试工具（如 WPA 和内核调试器）将显示名称。 

对于 PEP_NOTIFY_PPM_QUERY_VETO_REASON 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_enumerate_boot_vetoes"></a>PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES。

*数据*

NULL 指针值。

**备注**

通知 PEP 操作系统已准备好接受对 ProcessorIdleVeto 或 PlatformIdleVeto 的调用。 

Windows 电源管理框架（PoFx）在处理器初始化之后但在第一次空闲条目之前发送此通知，以指示 OS 已准备好接受对 ProcessorIdleVeto 或 PlatformIdleVeto 的调用。 PEP 可以在此通知的上下文中枚举任何启动时间 vetoes，操作系统保证它们在第一次尝试选择处理器、平台或协调空闲状态之前生效。 此通知没有关联的数据参数。 

对于 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_park_mask"></a>PEP_NOTIFY_PPM_PARK_MASK 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_PARK_MASK。

*数据*

指向 PEP_PPM_PARK_MASK 结构的指针。

**备注**

向 PEP 通知当前核心休止掩码。

Windows 电源管理框架（PoFx）会在运行时发送此通知，以通知当前核心休止掩码的 PEP。

对于 PEP_NOTIFY_PPM_PARK_MASK 通知，AcceptProcessorNotification 例程在 IRQL = DISPATCH_LEVEL 调用，在任何处理器上执行时可能会发送。

 
## <a name="pep_notify_ppm_park_selection_v2"></a>PEP_NOTIFY_PPM_PARK_SELECTION_V2 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_PARK_SELECTION_V2。

*数据*

指向 PEP_PPM_PARK_SELECTION_V2 结构的指针。

**备注**


通知 PEP，操作系统希望它选择一个首选核心集来阻止或防止中断。 如果未接受此通知，则操作系统将回退以发送 PEP_NOTIFY_PPM_PARK_SELECTION 通知。

在运行其性能检查算法时，OS 可能会多次发送 PEP_NOTIFY_PPM_PARK_SELECTION_V2 通知：每个寄存域中的每个 core 效能类有零次或多次，中断控制的时间为零次或多次。 为了帮助 PEP 提供对操作系统进行性能检查的一致响应，操作系统将提供提示通知的性能检查评估的基于中断时间的时间戳。 由一个性能检查评估生成的所有寄存选择通知都将具有相同的时间戳。 请注意，其余字段（Count、AdditionalUnparkedProcessors、EvaluationType 和处理器）可能会因在相同性能检查评估期间发送的通知而异，而 PEP 却无法假定它们将保持不变。 

对于 PEP_NOTIFY_PPM_PARK_SELECTION 通知，AcceptProcessorNotification 例程始终调用 IRQL = DISPATCH_LEVEL。

 
## <a name="pep_notify_ppm_perf_check_complete"></a>PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE。

*数据*

指向 PEP_PPM_PERF_CHECK_COMPLETE 结构的指针。

**备注**

通知 PEP 定期执行性能检查评估已完成。

Windows 电源管理框架（PoFx）在运行时发送此通知，以通知 PEP 每个检查评估的定期完成。

对于 PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 通知，AcceptProcessorNotification 例程在 IRQL = DISPATCH_LEVEL 调用，在任何处理器上执行时可能会发送。


## <a name="pep_notify_ppm_query_coordinated_dependency"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY。

*数据*

指向 PEP_PPM_QUERY_COORDINATED_DEPENDENCY 结构的指针。

**备注**

发送到 PEP 以查询每个协调的空闲状态的依赖项。

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以查询每个已协调空闲状态的依赖项的 PEP。 OS 将为依赖关系数组分配 MaximumDependencySize 元素。 PEP 必须填写 DependencySizeUsed 中使用的数组元素数。

如果要表示的依赖项在处理器上，则 PEP 会在 TargetProcessor 字段中填充目标处理器的 POHANDLE。 然后，ExpectedState 字段引用目标处理器上的处理器空闲状态的索引。 

如果要表示的依赖项位于其他协调的空闲状态，则 PEP 将为 TargetProcessor 填充 NULL。 然后，ExpectedState 字段指的是协调空闲状态的索引。 

每个依赖项都列出了一个选项菜单，该菜单允许 OS 用于满足依赖关系。 当处于空闲状态时，操作系统将通过检查每个索引的最高索引和最低索引的条件来尝试满足依赖关系。 如果满足依赖项的条件，则操作系统将考虑依赖关系。 如果无法满足任何条件，则不会满足依赖关系，也不能输入协调的空闲状态。

对于 PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_coordinated_state_name"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME。

*数据*

指向 PEP_PPM_QUERY_STATE_NAME 结构的指针。

**备注**

发送到 PEP 以查询有关特定协调或平台空闲状态的信息。

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以查询 PEP 以获取有关特定的协调或平台空闲状态的信息。 此通知将发送到每个状态两次，一次使用空的名称缓冲区检索名称所需的分配大小，使用非 NULL 名称缓冲区填充名称的内容。 名称应为可读的字符串，指示协调空闲状态的名称。 协调空闲状态应具有唯一的名称，但在多群集系统中，不同群集上的等效状态的名称可能相同。 WPA 和内核调试器等调试工具将在 "诊断" 中显示引用此协调/平台空闲状态的名称。

对于 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_coordinated_states"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES。

*数据*

指向 PEP_PPM_QUERY_COORDINATED_STATES 结构的指针。

**备注**

 在处理器初始化中用于查询所有已协调的空闲状态的属性。

Windows 电源管理框架（PoFx）会将此通知发送到 PEP 的处理器初始化，以查询所有协调的空闲状态的属性。 此通知将在 PEP 发送 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知之前发送。 如果接受，PEP 将使用协调式空闲状态接口，不会收到任何 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知。 如果未接受，则 PEP 使用平台空闲状态接口，操作系统将回退到使用 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知来查询协调的空闲状态。 

在所有处理器都注册到 PEP 之前，OS 将等待发送此通知。 

PEP 用有关协调空闲状态的信息填充状态结构。

协调空闲状态的顺序必须遵循以下规则： 

对于表示同一功能单元的不同电源状态的两种协调状态，应按顺序列出：从最浅（最高功率消耗/最小转换成本）到最深（最小功耗/最小转换成本）。 协调空闲状态可能仅依赖于具有较低索引的其他协调空闲状态。 两个不连续的协调空闲状态（即依赖于不连续的处理器集的两个协调的空闲状态）之间不需要顺序。

对于 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_query_processor_state_name"></a>PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME。

*数据*

指向 PEP_PPM_QUERY_STATE_NAME 结构的指针。

**备注**

发送到 PEP 以查询有关特定处理器空闲状态的信息。

Windows 电源管理框架（PoFx）将此通知发送到处理器初始化，以查询 PEP 以获取有关特定处理器空闲状态的信息。 此通知将发送到每个状态两次，一次使用空的名称缓冲区检索名称所需的分配大小，使用非 NULL 名称缓冲区填充名称的内容。 名称应为可读的字符串，指示协调空闲状态的名称。 协调空闲状态应具有唯一的名称，但在多群集系统中，不同群集上的等效状态的名称可能相同。 WPA 和内核调试器等调试工具将在 "诊断" 中显示引用此协调/平台空闲状态的名称。

对于 PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 通知，AcceptProcessorNotification 例程始终调用 IRQL = PASSIVE_LEVEL。


 
## <a name="pep_notify_ppm_enter_system_state"></a>PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE。

*数据*

指向 PEP_PPM_ENTER_SYSTEM_STATE 结构的指针。

**备注**

 PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 是一个可选通知，通知 PEP 系统即将进入系统电源状态。 系统完成将处理器转换为系统电源状态的所有被动级别工作后，会同时向所有处理器发送此通知。  

此通知将在 DISPATCH_LEVEL 发送，并在派单发送所有处理器。 此通知始终在目标处理器上执行。 

请注意，PEP 不得将此通知中的任何工作排队。 发送此通知后，处理器不会处理工作项、Dpc 等。 
 

DISPATCH_LEVEL
 
## <a name="pep_notify_ppm_perf_set_state"></a>PEP_NOTIFY_PPM_PERF_SET_STATE 

以下描述了[*AcceptProcessorNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/pepfx/nc-pepfx-pepcallbacknotifyppm)的参数。

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值**PEP_NOTIFY_PPM_PERF_SET_STATE**。

*数据*

指向[**PEP_PPM_PERF_SET_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/pep_x/ns-pep_x-_pep_ppm_perf_set_state)结构的指针。

**备注**

在运行时用于设置处理器的当前运行性能状态。 如果 PEP 具有可在不进行性能设置请求的情况下提升/降低性能的自治硬件，则应根据最小性能状态和/或最大性能状态限制来自自治硬件的请求，并以所需的性能状态。 否则，它应完全按所需的性能状态运行。  

此通知将在 DISPATCH_LEVEL 发送。 如果正在使用计划程序定向性能状态，则在处理此通知时，PEP 必须遵循3.3.6 部分中的限制。 它可以在任何处理器上执行时发送。 

 
## <a name="pep_notify_ppm_query_discrete_perf_states"></a>PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES。

*数据*

指向 PEP_PPM_QUERY_DISCRETE_PERF_STATES 结构的指针。
如果 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知指示对离散性能状态的支持，则在处理器初始化时使用它来查询 PEP 支持的离散性能状态的列表。  

性能状态列表应按从最快到最慢的顺序排列，每个性能状态映射到一个不同的性能值。 性能状态列表还应包括与 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知中列出的每个性能值匹配的条目。  此通知将在 PASSIVE_LEVEL 发送。 它可以在任何处理器上执行时发送。 


 
## <a name="pep_notify_ppm_query_domain_info"></a>PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO。

*数据*

指向 PEP_PPM_QUERY_DOMAIN_INFO 结构的指针。

**备注**

 查询有关性能域的信息的可选通知。  此通知将在 PASSIVE_LEVEL 发送。 它可以在任何处理器上执行时发送。



  
## <a name="pep_notify_ppm_resume_from_system_state"></a>PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE 

*柄*

一个 PEPHANDLE 结构，其中包含目标处理器的 PEP 的设备句柄。 如果通知不针对特定处理器，则为 NULL。

*通知*

值 PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE。

*数据*

指向 PEP_PPM_RESUME_FROM_SYSTEM_STATE 结构的指针。

**备注**

 一个可选通知，用于通知 PEP 系统系统刚恢复系统电源状态。 此通知会在处理器发布之前同时发送到所有处理器，以恢复被动级别工作。  此通知将在 DISPATCH_LEVEL 发送，并在派单发送所有处理器。 此通知始终在目标处理器上执行。 

 

