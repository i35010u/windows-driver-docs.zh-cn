---
title: 处理器电源管理 (PPM) 通知
description: PEP AcceptProcessorNotification 回调例程接收每个处理器电源管理 (PPM) 通知伴随通知参数指示类型的通知，以及指向数据结构的数据参数包含指定的通知类型的信息。
ms.assetid: 4BA89D0F-78F0-44DF-BC9B-0F9F3256CD59
keywords:
- AcceptProcessorNotification 回调
ms.date: 01/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a7e925c079a0b727c558c9020ce6a88e3fffaaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369139"
---
# <a name="processor-power-management-ppm-notifications"></a>处理器电源管理 (PPM) 通知
PEP AcceptProcessorNotification 回调例程接收每个处理器电源管理 (PPM) 通知伴随通知参数指示类型的通知，以及指向数据结构的数据参数包含指定的通知类型的信息。

在此调用，通知参数设置为 PEP_NOTIFY_PPM_XXX 常量值，该值指示通知类型。 数据参数指向与此通知类型相关联的 PEP_PPM_XXX 结构类型。

使用以下处理器电源管理 (PPM) 通知 Id AcceptProcessorNotification 回调例程。

## <a name="pepnotifyppmquerycapabilities"></a>PEP_NOTIFY_PPM_QUERY_CAPABILITIES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 的值。

指向 PEP_PPM_QUERY_CAPABILITIES 结构数据的指针。
通知 PEP 它正被查询 PEP 的电源管理功能。

PEP 查询其电源管理功能时，Windows 电源管理框架 (PoFx) 将发送此通知。 这发生在处理器初始化时，将在系统中发送的每个处理器。

与 x86/AMD64 处理器平台必须处理器性能控件使用 ACPI 接口。

若要发送 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知，PoFx 调用 PEP AcceptProcessorNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_PPM_QUERY_CAPABILITIES，且数据参数指向 PEP_PPM_QUERY_CAPABILITIES 结构。

对于 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryidlestates"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES 
通知 PEP_NOTIFY_PPM_QUERY_IDLE_STATES 的值。

指向 PEP_PPM_QUERY_IDLE_STATES 结构数据的指针。
有关空闲状态的信息通知 PEP。

若要发送 PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知，PoFx 调用 PEP AcceptProcessorNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_PPM_QUERY_IDLE_STATES，且数据参数指向 PEP_PPM_QUERY_IDLE_STATES 结构。

对于 PEP_NOTIFY_PPM_QUERY_IDLE_STATES 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmidleselect"></a>PEP_NOTIFY_PPM_IDLE_SELECT 
通知 PEP_NOTIFY_PPM_IDLE_SELECT 的值。

指向 PEP_PPM_IDLE_SELECT 结构数据的指针。
通知空闲选择的 PEP。

若要发送 PEP_NOTIFY_PPM_IDLE_SELECT 通知，PoFx 调用 PEP AcceptProcessorNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_PPM_IDLE_SELECT，且数据参数指向 PEP_PPM_IDLE_SELECT 结构。

对于 PEP_NOTIFY_PPM_IDLE_SELECT 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmidlecancel"></a>PEP_NOTIFY_PPM_IDLE_CANCEL 
通知 PEP_NOTIFY_PPM_IDLE_CANCEL 的值。

指向 PEP_PPM_IDLE_CANCEL 结构数据的指针。
通知取消操作的 PEP。

若要发送 PEP_NOTIFY_PPM_IDLE_CANCEL 通知，PoFx 调用 PEP AcceptProcessorNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_PPM_IDLE_CANCEL，且数据参数指向 PEP_PPM_IDLE_CANCEL 结构。

对于 PEP_NOTIFY_PPM_IDLE_CANCEL 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmidleexecute"></a>PEP_NOTIFY_PPM_IDLE_EXECUTE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_IDLE_EXECUTE 的值。

指向 PEP_PPM_IDLE_EXECUTE 或 PEP_PPM_IDLE_EXECUTE_V2 结构数据的指针。
发送到 PEP 转换为指定的空闲状态的当前处理器。

Windows 电源管理框架 (PoFx) PEP 转换为指定的空闲状态的当前处理器，以便向发送此通知。 

PEP 可以准备将其输入以前选择的空闲状态，包括通知的核心系统资源的睡眠转换可能会影响操作系统的硬件。 然后，它必须执行 halt 指令转换为空闲状态的处理器。 从空闲状态返回时，在 PEP 必须撤消硬件设置，包括通知的核心系统资源可能已变得时唤醒活动的 OS。 如果 PEP 不能执行的处理器 （和平台） 的空闲状态，则它必须返回返回的错误状态。

使用协调的空闲状态界面，操作系统将使用 PEP_PPM_IDLE_EXECUTE_V2 结构，其中包括使用空闲的转换将输入的协调空闲状态的列表在 CoordinatedStateCount 和 CoordinatedState 的字段。 如果有，PlatformState 字段将指定的最深的协调平台空闲状态正在输入。 

当未使用协调的空闲状态接口，操作系统将使用 PEP_PPM_IDLE_EXECUTE 结构。 

对于 PEP_NOTIFY_PPM_IDLE_EXECUTE 通知，AcceptProcessorNotification 例程调用都会在禁用。
 
## <a name="pepnotifyppmidlecomplete"></a>PEP_NOTIFY_PPM_IDLE_COMPLETE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 

通知 PEP_NOTIFY_PPM_IDLE_COMPLETE 的值。

数据的指针，指向 PEP_PPM_IDLE_COMPLETE 或 PEP_PPM_IDLE_COMPLETE_V2 结构...
通知已完成的空闲状态转换从唤醒当前处理器 PEP。

当前处理器唤醒从已完成的空闲状态转换时，Windows 电源管理框架 (PoFx) 将发送此通知。 如果平台执行平台空闲状态转换，第一个处理器来唤醒将指示正在退出的平台闲置状态。 根据平台空闲转换中使用类型，从平台空闲状态唤醒的第一个处理器可能不是同步的输入平台空闲状态的处理器。 

如果处理器正在执行深层空闲状态，PEP 不必须等待，直到它接收完成的通知，以还原 core 上下文，或通知操作系统核心资源已还原。 操作系统需要这些资源，以完成执行通知后已还原。 启用虚拟机监控程序，PEP 只会收到此通知在退出时，利用平台的空闲状态，以及设置为 PEP_PROCESSOR_IDLE_STATE_UNKNOWN ProcessorState 字段。 

使用协调的空闲状态界面，操作系统将使用 PEP_PPM_IDLE_COMPLETE_V2 结构，其中包括将退出空闲状态的转换的协调空闲状态的列表字段，CoordinatedStateCount 和 CoordinatedState 字段。 如果有，PlatformState 字段将指定正在退出后，最深协调的平台闲置状态。 请注意，是否使用松散的同步，协调退出此处理器的空闲状态的组可能会不同于的协调空闲状态，通过它，输入集。 

当未使用协调的空闲状态接口，操作系统将使用 PEP_PPM_IDLE_COMPLETE 结构。 

PEP_NOTIFY_PPM_IDLE_COMPLETE 通知 AcceptProcessorNotification 例程都会在禁用名为，始终执行目标处理器上。
 
## <a name="pepnotifyppmisprocessorhalted"></a>PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 的值。

指向 PEP_PPM_IS_PROCESSOR_HALTED 结构数据的指针。
发送到 PEP 来确定在其所选的空闲状态当前暂停指定的处理器。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP 来确定在其所选的空闲状态当前暂停指定的处理器。 操作系统将使用此通知来查看辅助处理器是否已完全完成转换为空闲时协调平台空闲状态。 PEP 必须保证目标处理器已达到其中平台空闲转换可以安全地出现 （例如，通过检查硬件寄存器，若要查看核心已暂停） 的状态。 一旦此通知指示在处理器处于空闲状态，该处理器必须唤醒除非操作系统的显式请求执行此操作。 

PEP 可能会收到此通知 IDLE_SELECT 和 IDLE_COMPLETE 通知之间的任何时间。 它确保接收此通知在空闲状态的转换过程最多一次。 

PEP_NOTIFY_PPM_IS_PROCESSOR_HALTED 通知，AcceptProcessorNotification 例程名为的任何 IRQL，都会在禁用在任何 irql，因此，永远不会执行目标处理器上。

&LT; = HIGH_LEVEL
 
## <a name="pepnotifyppminitiatewake"></a>PEP_NOTIFY_PPM_INITIATE_WAKE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。

通知 PEP_NOTIFY_PPM_INITIATE_WAKE 的值。

指向一个结构数据的指针。
发送到具有指定处理器 PEP，若要从不可中断的空闲状态，会启动其唤醒。

Windows 电源管理框架 (PoFx) 将此通知发送到具有指定处理器 PEP，若要从不可中断的空闲状态，会启动其唤醒。 PEP 必须返回目标处理器使用 NeedInterruptForCompletion 唤醒的状态。 如果处理器需要中断以完成从空闲状态唤醒，则返回 TRUE。 在这种情况下 PEP 必须确保目标处理器可处理此通知返回时中断。 如果目标处理器已在运行和/或最终将退出空闲状态 （和正在执行此操作） 而无需任何生成的软件中断，NeedInterruptForCompletion 应设置为 FALSE。


请注意 PEP 将不会同时收到此通知在同一处理器。
 

对于 PEP_NOTIFY_PPM_INITIATE_WAKE 通知，AcceptProcessorNotification 例程都会在禁用，调用任何 irql，永远不会执行目标处理器上。

&LT; = HIGH_LEVEL
 
## <a name="pepnotifyppmqueryfeedbackcounters"></a>PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 的值。

指向 PEP_PPM_QUERY_FEEDBACK_COUNTERS 结构数据的指针。
通知 PEP PEP 正被查询它支持的反馈计数器的列表。

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化来查询有关的反馈计数器，它支持列表 PEP。

对于 PEP_NOTIFY_PPM_QUERY_FEEDBACK_COUNTERS 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmfeedbackread"></a>PEP_NOTIFY_PPM_FEEDBACK_READ 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_FEEDBACK_READ 的值。

指向 PEP_PPM_FEEDBACK_READ 结构数据的指针。
通知 PEP 它正被查询的反馈计数器的当前值。

当它需要查询反馈计数器的当前值时，Windows 电源管理框架 (PoFx) 将发送此通知。 

可能都会在禁用发送此通知。 如果设置计数器的 Affinitized 字段，此通知目标处理器上执行。 否则，可能会从任何处理器执行此通知。

对于 PEP_NOTIFY_PPM_FEEDBACK_READ 通知，AcceptProcessorNotification 例程不能调用在 IRQL = DISPATCH_LEVEL。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmqueryperfcapabilities"></a>PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 的值。

指向 PEP_PPM_QUERY_PERF_CAPABILITIES 结构数据的指针。
通知 PEP 它正在查询的平台支持的性能范围。

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化查询支持的平台的性能范围。 PEP_PPM_QUERY_PERF_CAPABILITIES 结构的 DomainId 和 DomainMembers 字段用于表示对平台的性能状态域。 每个处理器是一个性能状态域的成员。 操作系统将确保性能域中的所有处理器一起都更改的性能。 

对于 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmperfconstraints"></a>PEP_NOTIFY_PPM_PERF_CONSTRAINTS 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 

通知 PEP_NOTIFY_PPM_PERF_CONSTRAINTS 的值。

指向 PEP_PPM_PERF_CONSTRAINTS 结构数据的指针。
通知 PEP 它正在查询的处理器的当前操作的约束。

当它想要检查处理器的当前操作约束时，Windows 电源管理框架 (PoFx) 将发送此通知。 PEP 启动一个请求，操作系统无法重新评估通过执行电源控制与该控件代码 GUID_PPM_PERF_CONSTRAINT_CHANGE 处理器的性能约束。 InBuffer 和 OutBuffer 必须为 NULL。 

PEP 必须等待，直到它接收一个处理器的 PEP_DPM_DEVICE_STARTED 通知才能发出的处理器的电源控制事务。 

对于 PEP_NOTIFY_PPM_PERF_CONSTRAINTS 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmperfset"></a>PEP_NOTIFY_PPM_PERF_SET 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_PERF_SET 的值。

指向 PEP_PPM_PERF_SET 结构数据的指针。
通知 PEP 应更改处理器的当前操作的性能。

Windows 电源管理框架 (PoFx) 将发送此通知，当它想要更改处理器的当前操作的性能。 任何处理器上执行时可能会发送此通知。

对于 PEP_NOTIFY_PPM_PERF_SET 通知，AcceptProcessorNotification 例程始终在调用 IRQL = DISPATCH_LEVEL。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmparkselection"></a>PEP_NOTIFY_PPM_PARK_SELECTION 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_PARK_SELECTION 的值。

指向 PEP_PPM_PARK_SELECTION 结构数据的指针。
通知 PEP OS 想让它选择的处理器内核停置首选的设置。

Windows 电源管理框架 (PoFx) 将发送此通知，以指示 PEP 来选择首选的一组核心驻留。

已重载 PEP_NOTIFY_PPM_PARK_SELECTION，若要执行两个函数： 

让 PEP 选择应停放哪些处理器 （从系统中的所有处理器的集），并应为 unparked。 让 PEP 选择哪些处理器 （所有处理器的 unparked 集中） 应会收到中断，哪些不应该接收中断。 Windows 不提供 PEP 来区分这两个操作系统执行的一种方法。 结果是，当 PEP 收到此通知包括一组给定的输入 （AdditionalUnparkedProcessors 计数和 PoPreference） 时，它应提供一致的输出 (PepPreference)，除非某些外部事件导致 PEP 首选项中的更改。 

对于 PEP_NOTIFY_PPM_PARK_SELECTION 通知，AcceptProcessorNotification 例程始终在调用 IRQL = DISPATCH_LEVEL。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmcststates"></a>PEP_NOTIFY_PPM_CST_STATES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_CST_STATES 的值。

指向 PEP_PPM_CST_STATES 结构数据的指针。
发送到 PEP 来指示的 ACPI 定义 C 的状态集支持的处理器。 

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP 来指示的 ACPI 定义 C 的状态集支持的处理器。 此通知将发送一次才能首次 PEP 接收 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知对于处理器，并再次任何时候该处理器接收 Notify(0x81)，该值指示 _CST 对象已更改。

对于 PEP_NOTIFY_PPM_CST_STATES 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryplatformstates"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 的值。

指向 PEP_PPM_QUERY_PLATFORM_STATES 结构数据的指针。
发送在处理器初始化查询 PEP 支持的平台闲置状态数。

Windows 电源管理框架 (PoFx) 将此通知发送到在处理器初始化 PEP 来查询它支持的平台闲置状态数。 在引导时发送此通知一次。 返回平台状态的一个非零数字后, PEP 然后可以开始在处理器空闲转换过程中选择平台空闲状态。

对于 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerylpsettings"></a>PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 
通知 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 的值。

指向 PEP_PPM_QUERY_LP_SETTINGS 结构数据的指针。
若要发送 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知，PoFx 调用 PEP AcceptProcessorNotification 回调例程。 在此调用，通知参数值为 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS，且数据参数指向 PEP_PPM_QUERY_LP_SETTINGS 结构。

对于 PEP_NOTIFY_PPM_QUERY_LP_SETTINGS 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryidlestatesv2"></a>PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 的值。

指向 PEP_PPM_QUERY_IDLE_STATES_V2 结构数据的指针。
在处理器初始化用于查询 PEP 支持的空闲状态的列表。

Windows 电源管理框架 (PoFx) 将此通知发送到在处理器初始化 PEP 来查询它所支持的空闲状态的列表。 

Count 成员指定空闲状态数组的大小。 处理器驱动程序将查询发送此通知之前的空闲状态与 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 数。 

它支持每个空闲状态有关的信息 IdleStates 数组中填充 PEP。 应降低成本的电源消耗/提高转换的顺序列出的空闲状态。 PEP 不需要报告相同的每个处理器的空闲状态的列表。 

对于 PEP_NOTIFY_PPM_QUERY_IDLE_STATES_V2 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryplatformstate"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 的值。

指向 PEP_PPM_QUERY_PLATFORM_STATE 结构数据的指针。
发送到 PEP 来查询单个平台空闲状态的属性。

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化查询单一平台空闲状态的属性。 

PEP_PPM_QUERY_PLATFORM_STATE 结构的状态索引参数指定的平台闲置状态对其进行查询的索引。 处理器驱动程序将查询发送此通知之前的受支持的平台与 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATES 空闲状态数。 处理器驱动程序然后将发送每个平台的空闲状态的一个 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 的通知。 处理器驱动程序将等待后用于发送此通知，直到所有处理器已都注册到 PEP。 

PEP 填充在状态结构平台闲置状态有关的信息。 平台空闲状态应降低成本的电源消耗/提高转换的顺序列出。 

对于 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmtestidlestate"></a>PEP_NOTIFY_PPM_TEST_IDLE_STATE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_TEST_IDLE_STATE 的值。

指向 PEP_PPM_TEST_IDLE_STATE 结构数据的指针。
用于测试是否可以在指定的处理器上输入指定的处理器和平台空闲状态。

Windows 电源管理框架 (PoFx) 将发送此通知来测试是否可以在指定的处理器上输入指定的处理器和平台空闲状态。 如果可以进入空闲状态，PEP 否决权代码 PEP_IDLE_VETO_NONE 中填充并完成空闲状态的转换。 如果出于某种原因，无法完成的空闲状态的转换，PEP 填充非零值否决权代码中。 

范围为 0xffffffff 0x80000000 中的重要否决权代码仅供 OS 使用和不能使用。
 

发送此通知后，操作系统已经证明与所选的处理器或平台空闲状态相关联的所有约束均已都满足，包括设备和处理器平台空闲状态转换的约束。 

尝试输入的任何处理器或平台空闲状态，除了处理器空闲状态与索引 0，它必须始终是 enterable 操作系统之前，将发送此通知。 完成与 PEP_IDLE_VETO_NONE 此通知不保证 OS 将输入指示的空闲状态。 此通知将发送具有禁用的中断。 此通知始终执行目标处理器上。 

对于 PEP_NOTIFY_PPM_TEST_IDLE_STATE 通知，AcceptProcessorNotification 例程调用都会在禁用。
 
## <a name="pepnotifyppmidlepreexecute"></a>PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 的值。

指向 PEP_PPM_IDLE_EXECUTE 或 PEP_PPM_IDLE_EXECUTE_V2 结构数据的指针。
发送到 PEP 以转换为指定的空闲状态对系统进行准备。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP 来准备系统转换为指定的空闲状态。 此通知的成功完成后，操作系统将转换处理器到空闲通过输入关联的 C-状态。 如果无法准备系统以输入 PEP 的处理器 （和平台） 空闲状态，则必须重新返回到错误状态。 

启用虚拟机监控程序，PEP 只会收到此通知到的平台闲置状态，并且具有设置为 PEP_PROCESSOR_IDLE_STATE_UNKNOWN ProcessorState 字段在输入时。 

使用协调的空闲状态界面，操作系统将使用 PEP_PPM_IDLE_EXECUTE_V2 结构，其中包括使用空闲的转换将输入的协调空闲状态的列表在 CoordinatedStateCount 和 CoordinatedState 的字段。 如果有，PlatformState 字段将指定的最深的协调平台空闲状态正在输入。 

当未使用协调的空闲状态接口，操作系统将使用 PEP_PPM_IDLE_EXECUTE 结构。 

PEP_NOTIFY_PPM_IDLE_PRE_EXECUTE 通知 AcceptProcessorNotification 例程都会在禁用名为，始终执行目标处理器上。
 
## <a name="pepnotifyppmupdateplatformstate"></a>PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 的值。

指向 PEP_PPM_QUERY_PLATFORM_STATE 结构数据的指针。
通知 PEP 处理器收到了 Notify(0x81) 更新平台空闲状态的特征。

Windows 电源管理框架 (PoFx) 将发送此通知时处理器收到了 Notify(0x81) 更新平台空闲状态的特征。 每种平台空闲状态，此通知将发送一次。 如果 PEP 不接受通知 （即返回 FALSE 从其 AcceptProcessorNotification 回调），然后从最新的平台空闲状态之前定义接受 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 或 PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 通知将被保留。 

此通知作为 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知使用相同的数据缓冲区。 

对于 PEP_NOTIFY_PPM_UPDATE_PLATFORM_STATE 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryplatformstateresidencies"></a>PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 的值。

指向 PEP_PPM_PLATFORM_STATE_RESIDENCIES 结构数据的指针。
通知 PEP，它应捕获自启动以来在每个平台的空闲状态所用的实际累计的时间。

Windows 电源管理框架 (PoFx) 将此通知发送到 PEP 来捕获自启动以来在每个平台的空闲状态所用的实际累计的时间。 在这种情况下，此查询是仅适用于平台的基础硬件可以自主决定输入不同于请求的 OS 平台闲置状态。 返回的值用于诊断目的，并指定时间的平台空闲状态驻留操作系统的视图有很大不同于平台的实际实现。 

计数状态数组，其中的元素索引对应于平台空闲状态索引中指定元素的数。 PEP 将填充与该匹配状态的实际驻留和转换计数的每个元素。 


请注意捕获此查询的累积的值应仅对应这些时段 PEP （或处理器驱动程序） 实际执行所在平台空闲状态转换。 这可确保 OS 计算的驻留和实际驻留之间的比较是有意义。
 

对于 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE_RESIDENCIES 通知，可以在任何 IRQL 调用 AcceptProcessorNotification 例程。
 
## <a name="pepnotifyppmqueryvetoreasons"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASONS 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_VETO_REASONS 的值。

指向 PEP_PPM_QUERY_VETO_REASONS 结构数据的指针。
用于查询多个 PEP ProcessorIdleVeto 和 PlatformIdleVeto 回调中使用的唯一否决权原因。 

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化来查询多个 PEP ProcessorIdleVeto 和 PlatformIdleVeto 回调中使用的唯一否决权原因。 此通知是可选的并可能通过 PEP 会被忽略。 

如果接受，PEP 被允许使用介于 1 和 VetoReasonCount，非独占，若要禁止任何处理器、 平台或协调空闲状态之间的否决权原因。 PEP 不是允许使用大于 VetoReasonCount 否决权原因。 操作系统预分配否决权跟踪结构，并保证所有处理器、 平台和协调的状态能都阻止回调时与 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 一起使用，将会成功。

如果 PEP 不接受此通知，PEP 可以与任何法律否决权原因使用 ProcessorIdleVeto 和 PlatformIdleVeto 回调。 操作系统不保证不会发生的分配失败或其他问题导致失败的回调。

对于 PEP_NOTIFY_PPM_QUERY_VETO_REASONS 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryvetoreason"></a>PEP_NOTIFY_PPM_QUERY_VETO_REASON 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_VETO_REASON 的值。

指向 PEP_PPM_QUERY_VETO_REASON 结构数据的指针。
有关特定否决权原因信息发送到查询到 PEP。

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化以查询有关特定否决权原因有关的信息。 此通知将发送两次的每个否决权原因、 NULLName 缓冲区来检索分配的大小所需的名称，使用一次，一次用于非 NULLName 缓冲区，以填充内容中的名称。 名称应为一个用户可读的字符串，指示此否决权原因表示哪种条件。 诊断原因未进入空闲状态时，调试工具，如 WPA 和内核调试程序将显示名称。 

对于 PEP_NOTIFY_PPM_QUERY_VETO_REASON 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmenumeratebootvetoes"></a>PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 的值。

NULL 指针值的数据。
通知操作系统已准备好接受调用 ProcessorIdleVeto 或 PlatformIdleVeto PEP。 

Windows 电源管理框架 (PoFx) 将发送此通知处理器初始化之后但在第一个空闲的条目之前以指示操作系统已准备好接受对 ProcessorIdleVeto 或 PlatformIdleVeto 的调用。 PEP 可以枚举此通知的上下文中的任何启动时 vetoes 和操作系统可以保证它们将会在第一次尝试选择处理器、 平台或协调空闲状态之前的生效。 此通知具有任何关联的数据参数。 

对于 PEP_NOTIFY_PPM_ENUMERATE_BOOT_VETOES 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmparkmask"></a>PEP_NOTIFY_PPM_PARK_MASK 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_PARK_MASK 的值。

指向 PEP_PPM_PARK_MASK 结构数据的指针。
通知当前的核心停车掩码 PEP。

Windows 电源管理框架 (PoFx) 在运行时发送此通知来通知当前的核心停车掩码 PEP。

对于 PEP_NOTIFY_PPM_PARK_MASK 通知，AcceptProcessorNotification 例程调用在 IRQL = DISPATCH_LEVEL 和任何处理器上执行时，可能会发送。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmparkselectionv2"></a>PEP_NOTIFY_PPM_PARK_SELECTION_V2 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_PARK_SELECTION_V2 的值。

指向 PEP_PPM_PARK_SELECTION_V2 结构数据的指针。
通知 PEP OS 想让它选择首选的一组核心停好或控制离开的中断。 如果不接受此通知，OS 会故障回复到发送 PEP_NOTIFY_PPM_PARK_SELECTION 通知。

多次运行时其性能检查算法，操作系统可能会发送 PEP_NOTIFY_PPM_PARK_SELECTION_V2 通知： 零个或多针对每个核心效率类中的每个 park 域，以及零个或更多次中断控制的时间。 若要为性能检查提供对 OS 的一致响应协助 PEP，操作系统将提供提示通知性能检查评估的中断时间基于时间戳。 从一个性能产生的所有 park 选择通知都检查评估将具有相同的时间戳。 请注意，其余字段 （计数、 AdditionalUnparkedProcessors、 EvaluationType 和处理器） 取决于在相同的性能检查评估期间发送的通知，PEP 不能假定它们将保持不变。 

对于 PEP_NOTIFY_PPM_PARK_SELECTION 通知，AcceptProcessorNotification 例程始终在调用 IRQL = DISPATCH_LEVEL。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmperfcheckcomplete"></a>PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 的值。

指向 PEP_PPM_PERF_CHECK_COMPLETE 结构数据的指针。
通知 PEP 定期性能检查评估已完成。

Windows 电源管理框架 (PoFx) 在运行时以通知每个定期检查已完成评估 PEP 发送此通知。

对于 PEP_NOTIFY_PPM_PERF_CHECK_COMPLETE 通知，AcceptProcessorNotification 例程调用在 IRQL = DISPATCH_LEVEL 和任何处理器上执行时，可能会发送。

DISPATCH_LEVEL
 
## <a name="pepnotifyppmquerycoordinateddependency"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 的值。

指向 PEP_PPM_QUERY_COORDINATED_DEPENDENCY 结构数据的指针。
每个协调的空闲状态的依赖项发送到查询到 PEP。

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化来查询每个协调的空闲状态的依赖项 PEP。 操作系统将为依赖项数组分配 MaximumDependencySize 元素。 PEP 必须填写 DependencySizeUsed 中使用了数组的元素数。

如果处理器上表达的依赖关系，在使用的目标处理器 POHANDLE TargetProcessor 字段中填写 PEP。 ExpectedState 字段然后引用的目标处理器上的处理器空闲状态的索引。 

如果所表示的依赖关系位于其他协调的空闲状态，PEP 填充 TargetProcessor 的空值。 ExpectedState 字段然后指协调的空闲状态的索引。 

每个依赖项列出了 OS 允许使用以满足依赖关系的选项的菜单。 当进入空闲状态，操作系统将尝试通过检查每个，从最高到最低的索引的索引的条件满足依赖关系。 如果满足依赖项条件，操作系统会视为满足的依赖关系。 如果可以满足任何条件，不符合依赖关系和可能未输入协调空闲状态。

对于 PEP_NOTIFY_PPM_QUERY_COORDINATED_DEPENDENCY 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerycoordinatedstatename"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 的值。

指向 PEP_PPM_QUERY_STATE_NAME 结构数据的指针。
有关特定的协调或平台空闲状态信息发送到查询到 PEP。

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化来查询有关特定的协调或平台空闲状态信息 PEP。 为每个状态、 使用一个空的名称的缓冲区来检索分配的大小所需的名称，一次，一次用于非 NULL 名称缓冲区两次发送此通知以填充内容中的名称。 名称应为一个用户可读的字符串，指示协调空闲状态的名称。 协调的空闲状态应具有唯一的名称，除在不同的群集上的等效州的名称可能是相同的多群集系统上。 WPA 和内核调试程序之类的调试工具将显示引用此协调/平台空闲状态的诊断中的名称。

对于 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATE_NAME 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerycoordinatedstates"></a>PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 的值。

指向 PEP_PPM_QUERY_COORDINATED_STATES 结构数据的指针。
在查询处理器初始化用于所有协调的空闲状态的属性。

Windows 电源管理框架 (PoFx) 将此通知发送到在所有协调空闲状态的属性的查询处理器初始化 PEP。 PEP 会发送 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知之前，会发送此通知。 如果接受，PEP 使用协调的空闲状态界面，并且不会收到任何 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 通知。 如果不接受，PEP 使用平台空闲状态界面，操作系统将回退到 PEP_NOTIFY_PPM_QUERY_PLATFORM_STATE 硄 查询用于协调空闲状态。 

操作系统将等待后用于发送此通知，直到所有处理器已都注册到 PEP。 

PEP 填充在有关协调空闲状态的信息状态结构。

协调的空闲状态的顺序必须遵循以下规则： 

两个协调表示不同的电源状态应从最亮的顺序列出的相同的功能单元的状态 （大多数电源消耗/最低转换成本） 到最深 （最少电能消耗/大多数转换成本）。 协调的空闲状态可能仅依赖其他具有较低索引的协调空闲状态。 两个非连续协调空闲状态 （即，两个协调空闲状态依赖于不相交集的处理器） 之间不存在所需的顺序。

对于 PEP_NOTIFY_PPM_QUERY_COORDINATED_STATES 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmqueryprocessorstatename"></a>PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 的值。

指向 PEP_PPM_QUERY_STATE_NAME 结构数据的指针。
有关特定处理器空闲状态信息发送到查询到 PEP。

Windows 电源管理框架 (PoFx) 发送此通知在处理器初始化来查询有关特定处理器空闲状态信息 PEP。 为每个状态、 使用一个空的名称的缓冲区来检索分配的大小所需的名称，一次，一次用于非 NULL 名称缓冲区两次发送此通知以填充内容中的名称。 名称应为一个用户可读的字符串，指示协调空闲状态的名称。 协调的空闲状态应具有唯一的名称，除在不同的群集上的等效州的名称可能是相同的多群集系统上。 WPA 和内核调试程序之类的调试工具将显示引用此协调/平台空闲状态的诊断中的名称。

对于 PEP_NOTIFY_PPM_QUERY_PROCESSOR_STATE_NAME 通知，AcceptProcessorNotification 例程始终在调用 IRQL = passive_level 调用。

PASSIVE_LEVEL
 
## <a name="pepnotifyppmentersystemstate"></a>PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 的值。

指向 PEP_PPM_ENTER_SYSTEM_STATE 结构数据的指针。
PEP_NOTIFY_PPM_ENTER_SYSTEM_STATE 是一个可选的通知，通知 PEP 系统即将进入系统电源状态。 此通知发送到的所有处理器同时后系统已完成转换到的系统电源状态的处理器的所有被动级别工作。  

使用所有处理器在调度 DISPATCH_LEVEL，在发送此通知。 此通知始终执行目标处理器上。 

请注意 PEP 必须排队此通知从任何工作。 处理器不会处理工作项、 Dpc，等后发送此通知。 
 

DISPATCH_LEVEL
 
## <a name="pepnotifyppmperfsetstate"></a>PEP_NOTIFY_PPM_PERF_SET_STATE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_PERF_SET_STATE 的值。

指向 PEP_PPM_PERF_SET_STATE 结构数据的指针。
在运行时用于设置处理器的当前操作的性能状态。 如果 PEP 能提高/降低性能没有性能集请求的自治硬件，它应限制从自治的硬件上的最小的性能状态和/或最大的性能状态，基于请求和目标所需性能状态。 否则，它应运行在完全的所需的性能状态。  

在 DISPATCH_LEVEL 发送此通知。 如果计划程序定向性能状态正在使用，PEP 必须遵守的第 3.3.6 部分中的限制时处理此通知。 它可能在任何处理器上执行时发送。 

DISPATCH_LEVEL
 
## <a name="pepnotifyppmquerydiscreteperfstates"></a>PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_DISCRETE_PERF_STATES 的值。

指向 PEP_PPM_QUERY_DISCRETE_PERF_STATES 结构数据的指针。
在查询处理器初始化一系列离散的性能状态 PEP 支持，如果使用 PEP_NOTIFY_PPM_QUERY_CAPABILITIES 通知指示支持离散的性能状态。  

性能状态列表应排序顺序为从最快到速度最慢，其中每个性能状态映射到一个明显的性能值。 性能状态列表还应包括 PEP_NOTIFY_PPM_QUERY_PERF_CAPABILITIES 通知中列出每个性能值相匹配的条目。  在 passive_level 调用发送此通知。 它可能在任何处理器上执行时发送。 

PASSIVE_LEVEL
 
## <a name="pepnotifyppmquerydomaininfo"></a>PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_QUERY_DOMAIN_INFO 的值。

指向 PEP_PPM_QUERY_DOMAIN_INFO 结构数据的指针。
一个可选的通知，查询以获取有关性能域的信息。  在 passive_level 调用发送此通知。 它可能在任何处理器上执行时发送。

PASSIVE_LEVEL

  
## <a name="pepnotifyppmresumefromsystemstate"></a>PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE 
处理 PEPHANDLE 结构，它包含的目标处理器 PEP 设备句柄。 如果该通知不具有特定处理器为目标，这将为 NULL。

通知 PEP_NOTIFY_PPM_RESUME_FROM_SYSTEM_STATE 的值。

指向 PEP_PPM_RESUME_FROM_SYSTEM_STATE 结构数据的指针。
通知系统只是已从系统电源状态恢复 PEP 可选通知。 此通知发送到的所有处理器同时发布处理器若要恢复被动工作之前。  使用所有处理器在调度 DISPATCH_LEVEL，在发送此通知。 此通知始终执行目标处理器上。 

DISPATCH_LEVEL
 

