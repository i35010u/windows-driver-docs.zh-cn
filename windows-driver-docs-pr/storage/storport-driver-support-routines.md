---
title: Storport 驱动程序支持例程
description: 了解 Storport 驱动程序例程，如直接内存访问和 i/o 请求处理支持例程。
ms.assetid: 15f20a83-43cc-40d4-8fa6-031affca5ee2
keywords:
- Storport 驱动程序支持例程
- 存储 WDK
- 存储支持例程
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1da0f52308cea75b2e3aeeb3c04a916f53b6acc3
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590385"
---
# <a name="storport-driver-support-routines"></a>Storport 驱动程序支持例程

此页列出系统提供的 Storport 驱动程序提供的支持例程。

有关 Storport 驱动程序微型端口例程的列表，请参阅 [Storport 微型端口驱动程序例程](storport-miniport-driver-routines.md)。

## <a name="direct-memory-access-support-routines"></a>直接内存访问支持例程

Storport 驱动程序提供以下 (DMA) 支持例程的直接内存访问。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortBuildScatterGatherList** | 为指定的数据缓冲区创建散点/集合列表。 |
| **StorPortGetScatterGatherList** | 检索指定 SCSI 请求块 (SRB) 的关联分散/收集列表。 |
| **StorPortPutScatterGatherList** | 释放与某个散点/集合列表关联的任何资源，该列表以前通过调用 **StorPortBuildScatterGatherList** 例程创建。 |

## <a name="general-support-routines"></a>常规支持例程

Storport 提供以下常规支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortDebugPrint** | 如果附加了调试器，则向内核调试器打印调试字符串。 |
| **StorPortEtwEvent2** | 向存储跟踪通道发布 Windows (ETW) 事件的事件跟踪。 小型端口可以记录两个常规用途的 ETW 参数。 ETW 参数以两个名称-值对的形式表示。 |
| **StorPortEtwEvent4** | 将 ETW 事件发布到存储跟踪通道。 小型端口可以记录四个常规用途的 ETW 参数。 ETW 参数以四个名称-值对的形式表示。 |
| **StorPortEtwEvent8** | 将 ETW 事件发布到存储跟踪通道。 小型端口可以记录8个常规用途 ETW 参数。 ETW 参数以8个名称-值对的形式表示。 |
| **StorPortGetActivityIdSrb** | 检索与请求块关联的 ETW 活动 ID。 |
| **StorPortGetDeviceObjects** | 返回与适配器设备堆栈关联的设备对象。 将返回的设备对象是适配器的功能和物理设备对象，以及功能设备对象附加到的设备对象。 |
| **StorPortGetSystemPortNumber** | 检索存储适配器的系统分配的端口号。 |
| **StorPortInitializeSListHead** | 初始化 Storport 管理的单向链接列表的头。 |
| **StorPortInterlockedFlushSList** | 从 Storport 管理的单向链接列表中移除所有项。 在多处理器系统上对列表的访问是同步的 |
| **StorPortInterlockedPopEntrySList** | 从 Storport 管理的单向链接列表的前面移除项。 在多处理器系统上，对列表的访问是同步的。  |
| **StorPortInterlockedPushEntrySList** | 将项插入到 Storport 托管的单链接列表前面。 在多处理器系统上，对列表的访问是同步的。 |
| **StorPortInvokeAcpiMethod** | 为存储设备执行 ACPI 方法。 |
| **StorPortIsCurrentOsInstallationUpgrade** | 检查 Windows 的当前安装是否从以前的版本升级。 |
| **StorPortIsDeviceOperationAllowed** | 允许微型端口确定是否允许对某个设备管理类执行操作。 |
| **StorPortLogError** | 通知端口驱动程序出现错误。 |
| **StorPortLogSystemEvent** | 授予微型端口驱动程序对 Windows 内核事件设施功能的完全访问权限，从而使微型端口驱动程序可以创建真正用于排查存储问题的事件日志条目。 它为 **StorPortLogError**提供了更好的替代方法。 |
| **StorPortQueryDepthSList** | 检索 Storport 管理的单向链接列表中的条目数。 |
| **StorPortQueryPerformanceCounter** | 查询并返回当前系统性能计数器的值。 |
| **StorPortQuerySystemTime** | 获取当前系统时间。 |
| **StorPortRegistryRead** | 读取指示的设备和值的注册表数据。 |
| **StorPortRegistryReadAdapterKey** | 读取注册表中位于 HKLM/CurrentControlSet/Enum//DeviceParameters/.... 的硬件或设备注册表适配器项 \<Instance path>|
| **StorPortRegistryWriteAdapterKey** | 写入注册表中 HKLM/CurrentControlSet/Enum//DeviceParameters/.... 处的硬件或设备注册表适配器项 \<Instance path> |
| **StorPortRegistryWrite** | 将指定缓冲区中包含的注册表数据从 ASCII 转换为 Unicode，然后将数据写入微型端口驱动程序的每 HBA 存储区。 |

## <a name="io-request-processing-support-routines"></a>I/o 请求处理支持例程

Storport 提供以下 i/o 请求处理支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortBusy** | 通知端口驱动程序适配器当前正忙，处理未处理的请求。 |
| **StorPortCompleteRequest** | 完成所有未完成的请求，将 SRB 状态值设置为 SrbStatus。 |
| **StorPortCompleteServiceIrp** | 当需要完成在其 HwStorProcessServiceRequest 回调例程中收到的请求时，由 Storport 虚拟微型端口驱动程序调用。 |
| **StorPortDeviceBusy** | 通知端口驱动程序指定的逻辑单元当前正忙，处理未处理的请求。 |
| **StorPortDeviceReady** | 通知端口驱动程序指示的逻辑单元已准备好处理新请求。 |
| **StorPortFreeWorker** | 释放先前由 **StorPortInitializeWorker** 例程分配的 Storport 工作项。 |
| **StorPortGetRequestInfo** | 检索与 SCSI 请求块关联的 IO 请求信息 (SRB) 并以 STOR_REQUEST_INFO 结构返回该信息。 |
| **StorPortInitializeWorker** | 创建在系统工作线程中运行的新的 Storport 工作项。 |
| **StorPortQueueWorkItem** | 计划在系统工作线程的上下文中执行的 Storport 工作项。 |
| **StorPortPause** | 暂停指定时间段内的适配器。 |
| **StorPortPauseDevice** | 在指定的时间段内暂停特定的逻辑单元设备。 |
| **StorPortReady** | 通知端口驱动程序适配器不再忙。 |
| **StorPortResume** | 恢复暂停的适配器。 |
| **StorPortResumeDevice** | 恢复先前暂停的逻辑单元。 |

## <a name="initialization-support-routines"></a>初始化支持例程

Storport 驱动程序提供以下初始化支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortEnablePassiveInitialization** | 使微型端口的 HwStorPassiveInitializeRoutine 回调例程在微型端口初始化期间 PASSIVE_LEVEL 执行。 |
| **StorPortGetActiveGroupCount** | 返回系统中存在的处理器组的数目。 |
| **StorPortGetActiveNodeCount** | 返回系统中存在的节点数。 |
| **StorPortGetBusData** | 检索初始化 HBA 所需的特定于总线的配置信息。 |
| **StorPortGetCurrentProcessorNumber** | 检索内核中的当前处理器编号。 |
| **StorPortGetGroupAffinity** | 在请求的组中构造活动处理器的掩码。 |
| **StorPortGetHighestNodeNumber** | 返回系统上可能的最大节点数。 |
| **StorPortGetLogicalProcessorRelationship** | 返回一个或多个指定类型的关系信息。 这些类型包括主机系统中的组、物理包和节点。 返回的信息包括由主机系统中的逻辑处理器组成的处理器关联掩码。 这些逻辑处理器共享指定的关系类型。 |
| **StorPortGetLogicalUnit** | 返回一个指向微型端口驱动程序的每个逻辑单元存储区域的指针。 |
| **StorPortGetNodeAffinity** |  (NUMA) 节点在请求的非一致性内存访问中构造活动处理器的掩码。 |
| **StorPortGetStartIoPerfParams** | 将给定 i/o 请求的性能参数置于 STARTIO_PERFORMANCE_PARAMETERS 结构中。 |
| **StorPortInitialize** | 初始化端口驱动程序参数和扩展数据。 **StorPortInitilize** 还保存从微型端口驱动程序中提供的适配器信息。 |
| **StorPortInitializePerfOpts** | 使用 PERF_CONFIGURATION_DATA 的结构初始化微型端口驱动程序和 Storport 驱动程序支持的性能优化。 |
| **StorPortSetAdapterBusType** | 用于根据适配器的当前配置调整适配器的 BusType。 如果将 BusType 设置为此例程，则可在无需重新安装驱动程序的情况下覆盖微型端口 INF 中的全局属性集。 这对于诸如支持不同总线类型的多个适配器的 RAID 支持或支持等方案非常有用。 |
| **StorPortSetBusDataByOffset** | 写入特定于总线的配置信息。 |
| **StorPortSetDeviceQueueDepth** | 设置指定设备的设备队列的最大深度。 |
| **StorPortSetPowerSettingNotificationGuids** | 启用微型端口来接收电源设置通知。 小型端口将注册一个 Guid 数组，这些 Guid 标识用于接收的电源更改通知的电源设置。 |
| **StorPortSetUnitAttributes** | 使用 Storport 驱动程序注册存储设备设备的电源属性。 |

## <a name="interrupt-support-routines"></a>中断支持例程

Storport 驱动程序提供以下中断支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortGetMSIInfo** | 为指定消息检索 (MSI) 信息的消息信号中断。 |
| **StorPortSynchronizeAccess** | 提供对微型端口驱动程序的设备扩展的同步访问。 |
| **StorPortInitializeDpc** |  (DPC 初始化 StorPort 延迟的过程调用 )  |
| **StorPortIssueDpc** | 发出 Storport DPC。 |
| **StorPortStallExecution** | 停止微型端口驱动程序。 |

## <a name="locking-support-routines"></a>锁定支持例程

Storport 驱动程序提供以下锁定支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortAcquireMSISpinLock** | 获取与指定的消息相关联 (MSI) 自旋锁的消息信号中断。 |
| **StorPortAcquireSpinLock** | 获取指定的旋转锁。 |
| **StorPortReleaseMSISpinLock** | 为指定的消息释放以前获取的 MSI 旋转锁。 |
| **StorPortReleaseSpinLock** | 释放 **StorPortAcquireSpinLock**获取的旋转锁。 |

## <a name="memory-management-support-routines"></a>内存管理支持例程

Storport 驱动程序提供了以下内存管理支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortAllocateContiguousMemorySpecifyCacheNode** | 分配一系列物理上不连续的非分页内存。 |
| **StorPortAllocateMdl** | 分配 MDL 以说明给定的非分页池内存。 |
| **StorPortAllocatePool** | 分配非连续的非分页池内存块。 |
| **StorPortAllocateRegistryBuffer** | 分配一个缓冲区，该缓冲区可用于读取和写入注册表数据。 |
| **StorPortBuildMdlForNonPagedPool** | 更新 MDL 以描述关联的非分页内存。 |
| **StorPortConvertUlongToPhysicalAddress** | 将无符号长地址转换为物理地址。 |
| **StorPortConvertPhysicalAddressToULong64** | 将物理地址转换为 ULONG64 值。 |
| **StorPortFreeMdl** | 释放 (MDL 的内存描述符列表，) 描述非分页池内存。 |
| **StorPortFreeContiguousMemorySpecifyCache** | 释放系统地址空间的非分页部分中的一系列非缓存内存。 |
| **StorPortFreePool** | 释放以前通过调用 **StorPortAllocatePool** 例程分配的内存块。 |
| **StorPortFreeRegistryBuffer** | 释放分配用于存储注册表数据的缓冲区。 |
| **StorPortGetDataInBufferMdl** | 返回与 SCSI 请求块的输入数据缓冲区关联的 MDL (SRB) 。 |
| **StorPortGetDataInBufferScatterGatherList** | 返回与 SCSI 请求块的输入数据缓冲区关联的散播聚集列表 (SRB) 。 |
| **StorPortGetDataInBufferSystemAddress** | 返回 SCSI 请求块 (SRB) 的输入数据缓冲区的系统地址。 |
| **StorPortGetOriginalMdl** | 返回与给定 SRB 关联的 MDL。 |
| **StorPortGetVirtualAddress** | 获取映射到指示的物理地址的虚拟地址。 |
| **StorPortGetPhysicalAddress** | 将给定的虚拟地址范围转换为 DMA 操作的物理地址范围。 |
| **StorPortGetSystemAddress** | 返回 (SRB) 的指定 SCSI 请求块的数据缓冲区的系统空间中的虚拟地址。 |
| **StorPortGetUncachedExtension** | 分配由 CPU 和设备共享的未缓存的公共缓冲区。 |
| **StorPortMarkDumpMemory** | 微型端口应标记用于转储文件或休眠文件的内存。 已标记的内存将保留，并在从休眠操作恢复后保持有效。 要标记的内存由在对 **StorPortMarkDumpMemory**的调用中使用的地址和范围长度来指定。 |
| **StorPortMoveMemory** | 将内存从一个缓冲区复制到另一个缓冲区。 |

## <a name="notification-support-routines"></a>通知支持例程

Storport 驱动程序提供以下通知支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortAsyncNotificationDetected** | 向 Storport 驱动程序通知存储设备状态更改事件。 |
| **StorPortNotification** | 向 Storport 驱动程序通知某些事件和条件。 |
| **StorPortStateChangeDetected** | 向 Storport 端口驱动程序通知 (LUN) 、主机总线适配器 (HBA) 端口或目标设备的逻辑单元号的状态更改。 |

## <a name="port-and-register-io-support-routines"></a>端口和注册 i/o 支持例程

Storport 驱动程序提供以下端口并注册 i/o 支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortGetDeviceBase** | 将 i/o 地址映射到系统地址空间。 |
| **StorPortFreeDeviceBase** | 释放由 StorPortGetDeviceBase 映射的一系列设备 i/o 内存。 |
| **StorPortReadPortBufferUchar** | 从指定的端口地址读取值 |
| **StorPortReadPortBufferUlong** | 从指定的端口地址中读取值。 |
| **StorPortReadPortBufferUshort** | 从指定的端口地址中读取值。 |
| **StorPortReadPortUchar** | 从指定的端口地址读取值 |
| **StorPortReadPortUlong** | 从指定的端口地址中读取值。 |
| **StorPortReadPortUshort** | 从指定的端口地址中读取值。 |
| **StorPortReadRegisterBufferUchar** | 从指定的寄存器地址中读取值。 |
| **StorPortReadRegisterBufferUlong** | 从指定的寄存器地址中读取值。 |
| **StorPortReadRegisterBufferUlong64** | 将来自指定64位寄存器地址的多个 ULONG64 值读取到缓冲区中。 |
| **StorPortReadRegisterBufferUshort** | 从指定的寄存器地址中读取值。 |
| **StorPortReadRegisterUchar** | 从指定的寄存器地址中读取值。 |
| **StorPortReadRegisterUlong** | 从指定的寄存器地址中读取值。 |
| **StorPortReadRegisterUlong64** | 从指定的64位寄存器地址读取64位值。 |
| **StorPortReadRegisterUshort** | 从指定的寄存器地址中读取值。 |
| **StorPortValidateRange** | 确定指定范围的 i/o 地址是否正在由另一个适配器使用。 此例程在 Windows NT 4.0 及更高版本的操作系统中已过时。 |
| **StorPortWritePortBufferUchar** | 将值写入指定的寄存器地址。 |
| **StorPortWritePortBufferUlong** | 将值写入指定的寄存器地址。 |
| **StorPortWritePortBufferUshort** | 将值写入指定的寄存器地址。 |
| **StorPortWritePortUchar** | 将值写入指定的寄存器地址。 |
| **StorPortWritePortUlong** | 将值写入指定的寄存器地址。 |
| **StorPortWritePortUshort** | 将值写入指定的寄存器地址。 |
| **StorPortWriteRegisterBufferUchar** | 将给定数量的无符号字节从缓冲区传输到 HBA。 |
| **StorPortWriteRegisterBufferUlong** | 将给定数目的 ULONG 值从缓冲区传输到 HBA。 |
| **StorPortWriteRegisterBufferUlong64** | 从指定的64位寄存器地址写入多个 ULONG64 值。 |
| **StorPortWriteRegisterBufferUshort** | 将给定数量的 USHORT 值从缓冲区传输到 HBA。 |
| **StorPortWriteRegisterUchar** | 将给定数量的字符值从缓冲区传输到指示的 HBA 注册地址。 |
| **StorPortWriteRegisterUlong** | 将 ULONG 值传输到指示的 HBA 注册地址。 |
| **StorPortWriteRegisterUlong64** | 将 ULONG64 值写入指定的寄存器地址。 |
| **StorPortWriteRegisterUshort** | 将 ULONG 值传输到指示的 HBA 注册地址。|

## <a name="runtime-power-management-support-routines"></a>运行时电源管理支持例程

Storport 驱动程序提供以下运行时电源管理支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortInitializePoFxPower** | 使用电源管理框架 (PoFx) 注册存储设备。 |
| **StorPortPoFxActivateComponent** | 递增存储设备上指定组件的激活引用计数。 |
| **StorPortPoFxIdleComponent** | 减少存储设备的指定组件的激活引用计数。 |
| **StorPortPoFxPowerControl** | 将电源控制请求发送到电源管理框架 (PoFx) 转发到 (PEP) 的 power engine 插件。 |
| **StorPortPoFxSetComponentLatency** | 指定在从空闲条件转换为指定的存储设备组件中的活动条件时可接受的最大延迟。 |
| **StorPortPoFxSetComponentResidency** | 设置在组件进入空闲状态后，存储设备组件可能保持空闲状态的估计时间。 |

## <a name="timer-support-routines"></a>计时器支持例程

Storport 驱动程序提供以下计时器支持例程。

| 例程所返回的值 | 说明 |
| ------- | ----------- |
| **StorPortFreeTimer** | 释放先前由 **StorPortInitializeTimer** 例程创建的 Storport 计时器上下文对象。 |
| **StorPortInitializeTimer** | 创建 Storport 计时器上下文对象。 |
| **StorPortRequestTimer** | 计划 Storport 计时器上下文对象的回调事件。 |
