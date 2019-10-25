---
title: 对管理启动驱动器的微型端口驱动程序的限制
description: 对管理启动驱动器的微型端口驱动程序的限制
ms.assetid: 78375e9b-8be9-4e64-b90e-cc8c4ab1751b
keywords:
- 存储微型端口驱动程序 WDK、启动驱动器
- 微型端口驱动程序 WDK 存储，启动驱动器
- 启动驱动器 WDK 存储
- 磁盘转储驱动程序 WDK 存储
- 转储模式 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70dce1a215b45e684beeeb1a68597a1d86b92118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842693"
---
# <a name="restrictions-on-miniport-drivers-that-manage-the-boot-drive"></a>对管理启动驱动器的微型端口驱动程序的限制


为启动设备管理适配器的存储微型端口驱动程序在系统崩溃期间受到特殊限制。 将系统的内存映像转储到磁盘时，微型端口驱动程序必须在不同环境中运行。 小型端口驱动程序、端口驱动程序和磁盘类驱动程序之间的正常通信被中断。 内核通过直接调用磁盘转储端口驱动程序*diskdump* （ATA 控制器的*dumpata* ），绕过文件系统和正常 i/o 堆栈来进行磁盘 i/o。 进而，磁盘转储驱动程序调用启动设备的微型端口驱动程序来处理所有 i/o 操作，而磁盘转储驱动程序会截获所有微型端口驱动程序对端口驱动程序的调用。

磁盘转储驱动程序提供了端口驱动程序提供的一组相同的支持例程，因此微型端口驱动程序应能够以使用端口例程的相同方式使用磁盘转储驱动程序例程。

但是，在转储模式下，管理磁盘转储路径中的适配器的微型端口驱动程序受到以下限制：

### <a name="span-idmem_usagespanspan-idmem_usagespanmemory-usage"></a><span id="mem_usage"></span><span id="MEM_USAGE"></span>内存使用情况

在系统崩溃期间，微型端口驱动程序必须对内存进行节约使用。 微型端口驱动程序可以为其设备和驱动程序扩展分配的非缓存内存量非常有限。 微型端口驱动程序不应尝试分配超过 32 kb 的内存。

### <a name="span-idaccessibilityspanspan-idaccessibilityspanaccessibility-of-the-boot-device"></a><span id="accessibility"></span><span id="ACCESSIBILITY"></span>启动设备的辅助功能

启动设备必须可在微型端口从初始化例程（为 StorPort 为 StorPort，[**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)用于 SCSI 端口[*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85)) ）返回之前访问。 初始化例程完成后，操作系统可能会在任何时间点将命令发送到引导设备。

### <a name="span-idbus_resetsspanspan-idbus_resetsspanbus-resets"></a><span id="bus_resets"></span><span id="BUS_RESETS"></span>总线重置

微型端口驱动程序应忽略用于重置总线的请求（[**HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus)为 STORPORT，SCSI 端口为[*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85)) ）。

### <a name="span-iddpcsspanspan-iddpcsspandeferred-procedure-calls-dpcs"></a><span id="dpcs"></span><span id="DPCS"></span>延迟的过程调用（Dpc）

StorPort 微型端口驱动程序不得尝试使用[**StorPortInitializeDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializedpc)初始化 DPC 例程（[**HwStorDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_dpc_routine)）。 在中断请求期间，通常排队等待执行到 DPC 例程的任何处理都必须在该请求的上下文中发生。

### <a name="span-idmultiple_requestsspanspan-idmultiple_requestsspanmultiple-requests-per-logical-unit"></a><span id="multiple_requests"></span><span id="MULTIPLE_REQUESTS"></span>每个逻辑单元的多个请求

磁盘转储端口驱动程序不会为每个逻辑单元发送多个请求。 因此，微型端口驱动程序为[**端口\_配置\_信息**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))的**MultipleRequestPerLu**成员分配的值并不重要。

### <a name="span-idpollingspanspan-idpollingspanpolling-and-time-checking"></a><span id="polling"></span><span id="POLLING"></span>轮询和时间检查

小型端口驱动程序不得依赖于时间检查例程，如在转储模式下运行时的[**ScsiPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportquerysystemtime)或[**StorPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportquerysystemtime) 。 由于微型端口驱动程序应始终使用端口驱动程序库例程来检查时间，因此最适用于微型端口驱动程序的最佳做法是在任何时候都排除使用[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)例程。

### <a name="span-idirqlspanspan-idirqlspaninterrupt-request-level"></a><span id="irql"></span><span id="IRQL"></span>中断请求级别

运行时端口驱动程序调用[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)和[*HWSCSIFINDADAPTER*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))的被动 IRQL。 但是，转储驱动程序调用的所有微型端口例程的 IRQL 高于被动。 因此，转储路径中的微型端口驱动程序必须避免必须在被动 IRQL 下执行的操作，如注册表访问。

### <a name="span-idtarget_and_lunspanspan-idtarget_and_lunspantarget-ids-and-logical-unit-numbers-luns"></a><span id="target_and_lun"></span><span id="TARGET_AND_LUN"></span>目标 Id 和逻辑单元号（Lun）

小型端口驱动程序在转储过程中不得为启动设备使用不同的目标 ID 和 LUN。

启动或转储路径中的存储微型端口驱动程序必须检测它们是否正在转储模式下运行。 操作系统可通过两种方式向存储微型端口驱动程序发出信号，指示微型端口驱动程序正在转储模式下运行，或者操作系统正在更改为休眠状态：

-   操作系统将**空**参数传递到微型端口驱动程序的*DriverEntry*例程。

-   在调用[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)或[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程时，磁盘转储端口驱动程序会在*ArgumentString*参数中传递字符串 "dump = 1"。

在调试程序中查看转储模式下的存储微型端口驱动程序的映像时，驱动程序名称将具有 "dump\_" 前缀。 如果微型端口驱动程序处于休眠模式，则驱动程序名称将具有前缀 "hiber\_"。

 

 




