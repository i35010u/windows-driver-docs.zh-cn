---
title: Surface 团队驱动程序开发最佳实践
description: Surface Team 驱动程序开发最佳方案-驱动程序开发人员导致的常见错误。
ms.assetid: f4847954-8e29-48bb-b9ae-873fc7c29b2d
keywords:
- 驱动程序开发最佳做法
ms.date: 08/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: b9d518d99da31984e5524016f432d5eaaa2d4a44
ms.sourcegitcommit: 73216293357f08eb00d8b154fa377a090644ca4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "94810121"
---
# <a name="surface-team-driver-development-best-practices"></a>Surface 团队驱动程序开发最佳实践

## <a name="introduction"></a>简介

这些驱动程序开发指南是由 Microsoft 的驱动程序开发者多年开发的。 随着时间的推移，在了解驱动程序的 misbehaved 和教训后，这些课程会被捕获并发展为这一组指导。 Microsoft Surface 硬件团队使用这些最佳做法来开发和维护支持独特 Surface 硬件体验的设备驱动程序代码。

与任何一组准则一样，将会出现合法的异常和替代方法，它们将同样有效。 请考虑将这些指导原则纳入开发标准，或者使用它们来根据你的开发环境和独特的需求来启动域特定的指导原则。 

## <a name="common-mistakes-made-by-driver-developers"></a>驱动程序开发人员的常见错误

### <a name="handling-io"></a>处理 i/o

1. 访问从 IOCTLs 检索的缓冲区，而不验证长度。 请参阅 [检查缓冲区大小失败](./failure-to-check-the-size-of-buffers.md)。
2. 在用户线程或随机线程上下文的上下文中执行阻塞 i/o。 请参阅 [内核调度程序对象简介](./introduction-to-kernel-dispatcher-objects.md)。
3. 在不超时的情况下将同步 i/o 发送到另一个驱动程序。 请参阅 [同步发送 I/o 请求](../wdf/sending-i-o-requests-synchronously.md)。
4. 使用非 io IOCTLs，而无需了解安全含义。 请参阅 [不使用缓冲的和直接](./using-neither-buffered-nor-direct-i-o.md)i/o。
5. 不会正确检查 [WdfRequestForwardToIoQueue](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) 或未处理故障的返回状态，从而导致放弃 WDFREQUESTs。
6. 使 WDFREQUEST 处于不可取消状态。 请参阅 [管理 I/o 队列](../wdf/managing-i-o-queues.md)、 [完成 I/o 请求](../wdf/completing-i-o-requests.md) 和 [取消 i/o 请求](../wdf/canceling-i-o-requests.md)。
7. 尝试使用 Mark/UnmarkCancelable 函数（而不是 IoQueues）管理取消。 请参阅 [框架队列对象](../wdf/framework-queue-objects.md)。
8. 不知道文件句柄清理和关闭操作之间的差异。 请参阅 [处理清理和关闭操作中的错误](./errors-in-handling-cleanup-and-close-operations.md)。
9. 忽视潜在递归的 i/o 完成，并从完成例程重新提交。
10. 不是对 WDFQUEUEs 的电源管理属性的明确。 不清楚地记录电源管理选项。 这是错误检查的主要原因0x9F： WDF 驱动程序中的 [驱动程序 \_ 电源 \_ 状态 \_ 故障](../debugger/bug-check-0x9f--driver-power-state-failure.md) 。 删除设备后，框架将在删除过程的不同阶段中从电源管理队列和非电源托管队列中清除 IO。 收到最终的 IRP \_ MN 删除设备时，将清除非电源管理的队列 \_ \_ 。 因此，如果在非电源管理的队列中保存 i/o，最好在 [EvtDeviceSelfManagedIoFlush](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush) 的上下文中显式清除 i/o 以避免死锁。
11. 未遵循处理 Irp 的规则。 请参阅 [处理清理和关闭操作中的错误](./errors-in-handling-cleanup-and-close-operations.md)。

### <a name="synchronization"></a>同步

1. 对不需要保护的代码持有锁。 当只需对少量的操作进行保护时，请勿持有整个函数的锁。
2. 调用的驱动程序持有锁。 这是死锁的主要原因。
3. 使用联锁基元创建锁定方案，而不是使用适当系统提供的锁定基元，例如互斥体、信号量和旋转锁。 请参阅 [Mutex 对象](./introduction-to-mutex-objects.md)、 [信号对象](./semaphore-objects.md) 和 [旋转锁简介](./introduction-to-spin-locks.md)中的介绍。
4. 使用旋转锁，其中某些类型的被动锁更合适。 请参阅 [快速 mutex 和受保护的 mutex](./fast-mutexes-and-guarded-mutexes.md) 和 [事件对象](./event-objects.md)。 有关锁的其他透视图，请查看 OSR 一文- [同步的状态](https://www.osr.com/nt-insider/2015-issue3/the-state-of-synchronization/)。
5. 选择 "WDF 同步和执行级别" 模型，而无需充分了解含义。 请参阅 [使用框架锁](../wdf/using-framework-locks.md)。 除非你的驱动程序直接与硬件交互，否则请避免选择执行 WDF 同步，因为这可能会导致递归导致死锁。
6. 在多个线程的上下文中获取 KEVENT、信号灯、ERESOURCE、UnsafeFastMutex，无需进入关键区域。 这样做可能会导致 DOS 攻击，因为持有其中一个锁定的线程可以被挂起。 请参阅 [内核调度程序对象简介](./introduction-to-kernel-dispatcher-objects.md)。
7. 在事件仍在使用时，在线程堆栈上分配 KEVENT 并返回到调用方。 通常在与 [IoBuildSyncronousFsdRequest](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest) 或 [IoBuildDeviceIoControlRequest](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)一起使用时完成。 这些调用的调用方应确保它们不会从堆栈展开，直到在完成 IRP 后，i/o 管理器发出事件信号。
8. 在调度例程中无限期等待。 通常，调度例程中的任何类型的等待都是一种不好的做法。
9. 如果在删除对象之前) 等等 = = NULL，则不能正确检查该 (对象的有效性。 这通常意味着作者对控制对象生存期的代码没有充分的了解。

### <a name="object-management"></a>对象管理

1. 未显式为 WDF 对象的父级。 请参阅 [框架对象简介](../wdf/introduction-to-framework-objects.md)。
2. 将 WDF 对象父对象改为 WDFDRIVER，而不是将其与提供更好的生存期管理的对象进行比较，并优化内存使用。
例如，将 WDFREQUEST 到 WDFDEVICE 而不是 IOTARGET。 请参阅 [使用常规框架对象](../wdf/using-general-framework-objects.md)、 [框架对象生命周期](../wdf/framework-object-life-cycle.md) 和 [框架对象的摘要](../wdf/summary-of-framework-objects.md)。
3. 不要对跨驱动程序访问的共享内存资源执行断开保护。 请参阅 [ExInitializeRundownProtection 函数](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializerundownprotection)。
4. 错误地将同一工作项排队，而上一个工作项已在队列中或已经在运行。 如果客户端假设每个排队的工作项将要执行，则这可能是一个问题。 请参阅 [使用框架](../wdf/using-framework-work-items.md)工作项。 有关队列工作项的详细信息，请参阅 (DMF) 项目中的 Driver Module Framework 中的 [dmf \_ QueuedWorkitem](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_QueuedWorkItem.md) 模块 <https://github.com/Microsoft/DMF> 。
5. 排队计时器在发布消息之前，应将计时器处理。 请参阅 [使用计时器](../wdf/using-timers.md)。
6. 在工作项中执行某项操作，该操作可阻止或需要无限长时间才能完成。
7. 设计一个解决方案，该解决方案会导致大量工作项排队。 如果攻击者可以控制操作 (例如，将中的 i/o 发送到为每个 i/o) 排队新工作项的驱动程序，则可能会导致系统或 DOS 攻击无响应。 请参阅 [使用框架工作项](../wdf/using-framework-work-items.md)。
8. 在删除对象之前，不会执行工作项 DPC 回调已经完成运行。 请参阅 [编写 DPC 例程](./guidelines-for-writing-dpc-routines.md) 和 [WdfDpcCancel 函数](/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpccancel)的准则。
9. 创建线程，而不是将工作项用于短持续时间/非轮询任务。 请参阅 [系统工作线程](./system-worker-threads.md)。
10. 删除或卸载驱动程序之前，不确保线程已完成运行。 有关线程断开同步的详细信息，请查看与 (DMF) 项目中的驱动程序模块框架中的 [DMF_Thread](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_Thread.md) 模块关联的代码 https://github.com/Microsoft/DMF 。 
11. 使用单个驱动程序管理不同但相互依赖并使用全局变量来共享信息的设备。

### <a name="memory"></a>内存

1. 如果可能，请不要将被动执行代码标记为可分页。 寻呼驱动程序代码可以减小驱动程序代码占用的大小，从而释放系统空间供其他用途使用。 请注意，将引发 IRQL = 调度级别的代码可分页标记为， \> \_ 或在引发的 IRQL 上调用。 了解 [何时应对代码和数据进行分页](./when-should-code-and-data-be-pageable-.md) ，并 [使驱动程序可分页](./making-drivers-pageable.md) 并 [检测可分页的代码](./detecting-code-that-can-be-pageable.md)。
2. 在堆栈上声明大型结构应使用堆/poolinstead。 请参阅 [使用 KernelStack](./using-the-kernel-stack.md) 和 [分配 System-Space 内存](./allocating-system-space-memory.md)。
3. 不必要地对 WDF 对象上下文进行清零。 这可能表示在自动将内存归零时，缺少清晰的情况。

### <a name="general-driver-guidelines"></a>一般驱动程序指南

1. 混合 WDM 和 WDF 基元。 使用可以使用 WDF 基元的 WDM 基元。 使用 WDF 基元可防止问题、改进调试，更重要的是，使驱动程序可 usermode。
2. 命名 FDOs 并在不需要时创建符号链接。 请参阅 [管理驱动程序访问控制](../driversecurity/driver-security-checklist.md#manage-driver-access-control)。
3. 从示例驱动程序复制粘贴并使用 Guid 和其他常量值。
4. 请考虑在驱动程序项目中使用驱动程序模块框架 (DMF) 开放源代码。 DMF 是用于实现 WDF 驱动程序开发人员额外功能的 WDF 扩展。 请参阅 [驱动程序模块框架简介](https://blogs.windows.com/windowsdeveloper/2018/08/15/introducing-driver-module-framework/)。
5. 使用注册表作为进程间通知机制或邮箱。 有关替代方法，请参阅 DMF 项目中提供的 [dmf \_ NotifyUserWithEvent](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_NotifyUserWithEvent.md) 和 [dmf \_ NotifyUserWithRequest](https://github.com/Microsoft/DMF/blob/master/Dmf/Modules.Library/Dmf_NotifyUserWithRequest.md) 模块 <https://github.com/Microsoft/DMF> 。
6. 假定注册表的所有部分在系统的早期启动阶段都可用于访问。
7. 依赖于另一驱动程序或服务的加载顺序。 由于可以在您的驱动程序控制外更改加载顺序，因此这可能会导致驱动程序最初有效，但稍后将无法预测的模式。
8. 重新创建已可用的驱动程序库，如 WDF 为在 [驱动程序中支持 pnp 和电源管理中](../wdf/supporting-pnp-and-power-management-in-your-driver.md) 所述的 Pnp 提供支持或在总线接口中提供的驱动程序库，如 [使用用于驱动程序到驱动程序通信的总线接口](https://www.osr.com/nt-insider/2014-issue2/using-bus-interfaces-driver-driver-communication/)OSR 一文中所述。

### <a name="pnppower"></a>PnP/Power

1. 以非 pnp 友好方式与其他驱动程序交互-未注册 pnp 设备更改通知。 请参阅 [注册设备接口更改通知](./registering-for-device-interface-change-notification.md)。
2. 创建 ACPI 节点以枚举设备，并在其中创建电源依赖关系，而不是使用总线驱动程序或系统提供的软件设备创建接口到 PNP 和电源依赖项。 请参阅 [功能驱动程序中的支持 PnP 和电源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)。
3. 将设备标记为不 disableable-对驱动程序更新强制重新启动。
4. 在设备管理器中隐藏设备。 请参阅 [隐藏设备管理器的设备](./hiding-devices-from-device-manager.md)。
5. 假设该驱动程序将仅用于设备的一个实例。
6. 假定驱动程序永远不会被卸载。 请参阅 [PnP 驱动程序的卸载例程](./pnp-driver-s-unload-routine.md)。
7. 未处理假接口到达通知。 这种情况可能会发生，驱动程序应安全地处理这种情况。
8. 不实现 S0 空闲电源策略，这对于 DRIPS 约束或子项的设备很重要。 请参阅 [支持空闲电源关闭](../wdf/supporting-idle-power-down.md)。
9. 不检查 [WdfDeviceStopIdle](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 返回状态将导致由于 WdfDeviceStopIdle/ResumeIdle 不平衡和最终的 9f bug 检查而导致的电源引用泄漏。
10. 由于资源重新平衡，不知道 PrepareHardware/ReleaseHardware 只能调用一次。 应限制这些回调来初始化硬件资源。 请参阅 [.Evt \_ WDF \_ 设备 \_ 准备 \_ 硬件](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)。
11. 使用 PrepareHardware/ReleaseHardware 分配软件资源。 如果分配的资源需要与硬件交互，则应在 AddDevice 中或在 SelfManagedIoInit 中完成对设备的静态软件资源分配。 请参阅 [.Evt \_ WDF \_ 设备 \_ 自行 \_ 管理 \_ IO \_ INIT](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_init)。

### <a name="coding-guidelines"></a>编码指导原则

1. 不使用安全字符串和整数函数。 请参阅 [使用安全字符串函数](./using-safe-string-functions.md) 和 [使用安全整数函数](./ntintsafe-design-guide.md)。
2. 不使用 typedef 定义常量。
3. 使用全局和静态变量。 避免在全局中存储每个设备上下文。 Globals 用于在多个设备实例之间共享信息。 作为替代方法，请考虑使用 WDFDRIVER 对象上下文在多个设备实例之间共享信息。
4. 不使用变量的描述性名称。
5. 命名变量不一致-区分大小写。 在对现有代码进行更新时，未遵循现有编码样式。 例如，对不同函数中的公共结构使用不同的变量名称。
6. 不注释重要的设计选择-电源管理、锁、状态管理、工作项、Dpc、计时器、全局资源使用情况、资源预分配、复杂的表达式/条件语句。
7. 对从被调用的 API 名称中显而易见的东西进行注释。 将注释设为与函数名称等效的英语 (例如，在调用 WdfDeviceCreate 时编写注释 "创建设备对象") 。
8. 请勿创建具有返回调用的宏。 请参阅 [函数 (c + +) ](/cpp/cpp/functions-cpp)。
9.  (SAL) 不含或不完整的源代码批注。 请参阅 [适用于 Windows 驱动程序的 SAL 2.0 批注](../devtest/sal-2-annotations-for-windows-drivers.md)。
10. 使用宏而不是内联函数。
11. 使用 c + + 时，使用常量的宏替代[constexpr](/cpp/cpp/constexpr-cpp)
12. 用 C 编译器而不是 c + + 编译器编译驱动程序，以确保获得强类型检查。

### <a name="error-handling"></a>错误处理

1. 不报告关键驱动程序错误，并正确地将设备标记为无法正常工作。
2. 不返回会转换为有意义的 WIN32 错误状态的相应 NT 错误状态。 请参阅 [使用 NTSTATUS 值](./using-ntstatus-values.md)。
3. 不使用 NTSTATUS 宏来检查系统函数的返回状态。
4. 不在需要时断言状态变量或标志。
5. 检查指针是否有效，然后再访问它以解决争用情况。
6. 对 NULL 指针进行断言。 如果尝试使用 NULL 指针访问内存窗口，将会检查错误。 Bug 检查的参数将提供修复 null 指针所需的信息。 加班，当多个不需要的 ASSERT 语句添加到代码中时，它们会消耗内存并使系统变慢。
7. 对对象上下文指针进行断言。 驱动程序框架保证对象将始终通过上下文进行分配。

### <a name="tracing"></a>跟踪

1. 不要定义 WPP 自定义类型，并在跟踪调用中使用它来获取用户可读的跟踪消息。 请参阅向 [Windows 驱动程序添加 WPP 软件跟踪](../devtest/adding-wpp-software-tracing-to-a-windows-driver.md)。
2. 不使用 IFR 跟踪。 请参阅 [在 KMDF 和 UMDF 2 驱动程序中使用即时 Trace 录像机 (IFR) ](../wdf/using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)。
3. 在 WPP 跟踪调用中调用函数名称。 WPP 已跟踪函数名称和行号。
4. 不要使用 ETW 事件来测量影响事件的性能和其他关键用户体验。 请参阅 [将事件跟踪添加到 Kernel-Mode 驱动程序](../devtest/adding-event-tracing-to-kernel-mode-drivers.md)。
5. 不报告事件日志中的严重错误，并正确地将设备标记为不起作用。

### <a name="verification"></a>验证

1. 在开发和测试期间，不会同时运行带有标准设置和高级设置的驱动程序验证程序。 请参阅 [驱动程序验证](../devtest/driver-verifier.md)器。 在 "高级" 设置中，建议启用除与资源不足模拟相关的规则之外的所有规则。 更可取的方法是隔离运行低资源模拟测试，以便更轻松地调试问题。
2. 如果未对驱动程序或设备类运行 DevFund 测试，驱动程序将成为启用了高级验证程序设置的一部分。 请参阅 [如何通过命令行运行 DevFund 测试](../devtest/run-devfund-tests-via-the-command-line.md)。
3. 未验证驱动程序是否符合要求 HVCI。 请参阅 [评估要求 hvci 驱动程序兼容性](../driversecurity/use-device-guard-readiness-tool.md)。
4. 在开发和测试用户模式驱动程序的过程中，不会在 WUDFhost.exe 上运行 AppVerifier。 请参阅 [应用程序验证工具](../devtest/application-verifier.md)。
5. 在运行时不使用[ \! wdfpoolusage](../debugger/-wdfkd-wdfpoolusage.md)调试器扩展来检查内存使用情况，确保不会放弃 WDF 对象。 内存、请求和工作项是这些问题的常见受害者。
6. 不要使用[ \! wdfkd](../debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-.md)调试器扩展来检查对象树，以确保对象的父级正确并检查主要对象（如 WDFDRIVER、WDFDEVICE、IO）的特性。