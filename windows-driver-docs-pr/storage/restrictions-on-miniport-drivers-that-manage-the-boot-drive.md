---
title: 对管理启动驱动器的微型端口驱动程序的限制
description: 对管理启动驱动器的微型端口驱动程序的限制
ms.assetid: 78375e9b-8be9-4e64-b90e-cc8c4ab1751b
keywords:
- 存储微型端口驱动程序 WDK、 启动驱动器
- 微型端口驱动程序 WDK 存储，启动驱动器
- 启动驱动器 WDK 存储
- 磁盘转储驱动程序 WDK 存储
- 转储模式 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f11d76dcb70bd4a43e274a42d0596a4cf1e84a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373208"
---
# <a name="restrictions-on-miniport-drivers-that-manage-the-boot-drive"></a>对管理启动驱动器的微型端口驱动程序的限制


系统崩溃期间，存储微型端口驱动程序，用于管理启动设备的适配器会受到特殊限制。 时转储到磁盘的系统的内存映像，微型端口驱动程序必须运行在不同环境中。 微型端口驱动程序、 端口驱动程序和磁盘类驱动程序之间的常见通信会中断。 内核执行通过直接调用磁盘转储端口驱动程序，磁盘 I/O *diskdump.sys* (*dumpata.sys* ATA 控制器)，跳过文件系统和正常 I/O 堆栈。 磁盘转储驱动程序，都依次调用启动设备微型端口驱动程序来处理所有 I/O 操作，以及磁盘转储驱动程序会截获所有对端口驱动程序微型端口驱动程序的调用。

磁盘转储驱动程序提供支持例程的端口驱动程序提供，一的组相同，因此微型端口驱动程序应该能够在相同的方式，它使用端口例程中使用磁盘转储驱动程序例程。

但是，管理磁盘转储路径中的适配器的微型端口驱动程序是在转储模式下的以下限制：

### <a name="span-idmemusagespanspan-idmemusagespanmemory-usage"></a><span id="mem_usage"></span><span id="MEM_USAGE"></span>内存使用情况

微型端口驱动程序必须在系统崩溃期间地节约使用的内存。 微型端口驱动程序可以为其设备和驱动程序扩展分配的非缓存内存量是非常有限。 微型端口驱动程序不应尝试分配的内存超过 32 千字节。

### <a name="span-idaccessibilityspanspan-idaccessibilityspanaccessibility-of-the-boot-device"></a><span id="accessibility"></span><span id="ACCESSIBILITY"></span>启动设备的可访问性

启动设备之前从初始化例程返回微型端口必须可访问性 ([**HwStorInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize) StorPort 的并[ *HwScsiInitialize* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85)) SCSI 端口)。 初始化例程完成后，操作系统可能会将命令发送到任何位置启动设备。

### <a name="span-idbusresetsspanspan-idbusresetsspanbus-resets"></a><span id="bus_resets"></span><span id="BUS_RESETS"></span>总线重置

微型端口驱动程序应忽略请求重置总线 ([**HwStorResetBus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus) StorPort 的并[ *HwScsiResetBus* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85))的 SCSI端口）。

### <a name="span-iddpcsspanspan-iddpcsspandeferred-procedure-calls-dpcs"></a><span id="dpcs"></span><span id="DPCS"></span>延迟的过程调用 (Dpc)

StorPort 微型端口驱动程序不能尝试初始化 DPC 例程 ([**HwStorDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_dpc_routine)) 与[ **StorPortInitializeDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitializedpc)。 任何处理通常排队等待到 DPC 例程期间的中断请求的执行，在这种情况下，必须在该请求的上下文中。

### <a name="span-idmultiplerequestsspanspan-idmultiplerequestsspanmultiple-requests-per-logical-unit"></a><span id="multiple_requests"></span><span id="MULTIPLE_REQUESTS"></span>每个逻辑单元的多个请求

磁盘转储端口驱动程序不发送每个逻辑单元的多个请求。 因此，它并不重要的微型端口驱动程序将分配给哪些值**MultipleRequestPerLu**的成员[**端口\_配置\_信息**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)).

### <a name="span-idpollingspanspan-idpollingspanpolling-and-time-checking"></a><span id="polling"></span><span id="POLLING"></span>轮询间隔和时间检查

微型端口驱动程序必须不依赖时检查例程，如[ **ScsiPortQuerySystemTime** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportquerysystemtime)或[ **StorPortQuerySystemTime** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportquerysystemtime)同时在转储模式下运行。 使用中排除的微型端口驱动程序的最佳实践[ **KeQuerySystemTime** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerysystemtime)例程，在任何时间，因为微型端口驱动程序应始终使用端口驱动程序库例程来检查的时间。

### <a name="span-idirqlspanspan-idirqlspaninterrupt-request-level"></a><span id="irql"></span><span id="IRQL"></span>中断请求级别

运行时端口驱动程序调用[ **HwStorFindAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)并[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))在被动 irql 下完成。 但是，转储驱动程序调用的 IRQL 高于被动所有微型端口例程。 因此，转储路径中的微型端口驱动程序必须避免的操作，例如注册表访问，必须执行在被动 irql 下完成。

### <a name="span-idtargetandlunspanspan-idtargetandlunspantarget-ids-and-logical-unit-numbers-luns"></a><span id="target_and_lun"></span><span id="TARGET_AND_LUN"></span>目标 Id 和逻辑单元号 (Lun)

微型端口驱动程序必须不用于不同的目标 ID 和 LUN 启动设备在转储过程。

启动或转储路径中的存储微型端口驱动程序必须检测其能否运行在转储模式下。 有两种操作系统发出信号的存储微型端口驱动程序，在转储模式下运行的微型端口驱动程序或操作系统进入休眠状态的方法：

-   操作系统将传递**NULL**微型端口驱动程序的参数*DriverEntry*例程。

-   磁盘转储端口驱动程序将传递的字符串"转储 = 1"中*ArgumentString*参数时，它调用[ **HwStorFindAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)或[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))例程。

当您查看转储模式中的存储微型端口驱动程序的映像在调试器中时，驱动程序名称将具有前缀"转储\_"。 如果微型端口驱动程序处于休眠模式下，驱动程序名称将包含前缀为"休眠\_"。

 

 




