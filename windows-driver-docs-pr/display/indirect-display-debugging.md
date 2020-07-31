---
title: 调试间接显示驱动程序
description: 介绍间接显示驱动程序的调试技术
ms.assetid: a343812d-03d0-4a95-9c36-7e6b5a404088
ms.date: 07/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8ae9551a699e3015718bcffeca075e4a6ffd4166
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402288"
---
# <a name="debugging-indirect-display-drivers"></a>调试间接显示驱动程序

间接显示驱动程序（IDDs）是一种 UMDF 驱动程序，因此，UMDF 调试文档（如[确定导致 UMDF 驱动程序无法加载或启动 Umdf 设备](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)时）是一个很好的起点。  本页提供间接显示特定的调试信息。

## <a name="registry-control"></a>注册表控件

间接显示驱动程序类扩展（IccDx）具有一些可用于帮助调试 IDDs 的注册表设置。 所有注册表值都位于**HKLM\System\CurrentControlSet\Control\GraphicsDrivers**注册表项下。

| 值名称               | 详细信息 |
|--------------------------|---------|
| TerminateIndirectOnStall | 如果此值为零，则将禁用终止该驱动程序的监视程序（如果它未在10秒内提供可用帧）。 任何其他值都将使监视程序处于启用状态。 |
| IddCxDebugCtrl           | 启用 IddCx 的不同调试方面的位域。 请参阅下表。 |

> [!NOTE]
>
> 如果将 TerminateIndirectOnStall 注册表值用于禁用监视程序，则 HLK 测试将失败。

### <a name="iddcxdebugctrl-values"></a>IddCxDebugCtrl 值

| IddCxDebugCtrl 中的位 | 含义  |
|:---------------------:|----------|
| 0x0001 | 当 IddCx 检测到错误时中断到调试器 |
| 0x0002 | 加载 IddCx 时中断调试器 |
| 0x0004 | 在卸载 IddCx 时中断到调试器 |
| 0x0008 | 调用 IddCx DriverEntry 时中断调试器 |
| 0x0010 | 在调用驱动程序绑定时中断到调试器 |
| 0x0020 | 在调用驱动程序启动时中断到调试器 |
| 0x0040 | 调用驱动程序绑定时中断调试器 |
| 0x0080 | 禁用 DDI 监视程序，在 DDI 调用中终止驱动程序的时间过长 |
| 0x0100 | 未使用 |
| 0x0200 | 启用调试覆盖，如下所示 |
| 0x0400 | 覆盖帧中脏 rect 上方的彩色 alpha 框;需要设置0x0200 |
| 0x0800 | 将 pref 统计信息覆盖到帧;需要设置0x0200 |

> [!NOTE]
>
> 要使任何覆盖功能正常工作，必须使用**D3D11_CREATE_DEVICE_BGRA_SUPPORT**标志创建驱动程序创建的 Direct3D 设备并将其传递给[**IddCxSwapChainSetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxswapchainsetdevice) 。

## <a name="iddcx-wpp-traces"></a>IddCx WPP 跟踪

Iddcx 使用[WPP 基础结构](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)记录调试信息。 可以将 WPP 信息捕获到文件，并且在此捕获正在进行时，可以在内核调试器中显示它。

### <a name="capturing-iddcx-wpp-tracing"></a>捕获 IddCx WPP 跟踪

可以通过多种方式来启用 WPP 跟踪。 一种简便方法是使用[*logman.exe*](https://docs.microsoft.com/windows-server/administration/windows-commands/logman)程序中的生成。 如果将以下行复制到批处理文件中，并在提升的命令提示符下运行，则会将 IddCx WPP 跟踪收集到*IddCx*文件中。

```console
@echo off  
echo Starting WPP tracing....
logman create trace IddCx -o IddCx.etl -ets -ow -mode sequential -p  {D92BCB52-FA78-406F-A9A5-2037509FADEA} 0x4f4 0xFF
echo Tracing enabled
pause
echo Stopping WPP tracing....
logman -stop IddCx -ets
```

#### <a name="controlling-what-is-captured"></a>控制捕获的内容

*logman.exe* （在本例中为0x4f4）的 Flags 参数控制 WPP 消息 IddCx 日志。  此的含义值在 Windows 版本19041及更高版本中发生了更改。

##### <a name="flags-meaning-for-windows-build-19041-and-above"></a>Windows 版本19041及更高版本的标志含义

标志是一个位域，其中每个位控制是否捕获消息类型。

| 标志位 | 捕获的消息类型  |
|:---------:|------------------------|
| 0x001     | 未使用  |
| 为 0x002     | 未使用  |
| 0x004     | 错误  |
| 0x008     | 良性错误，如启用了调试覆盖，但未设置 D3D11_CREATE_DEVICE_BGRA_SUPPORT |
| 0x010     | IddCx 对象  |
| 0x020     | UMDF 框架调入 IddCx |
| 0x040     | 从 IddCx 到驱动程序的 DDI 调用 |
| 0x080     | 从驱动程序到 IddCx 的低频率调用 |
| 0x100     | 从驱动程序到 IddCx 的高频帧相关调用 |
| 0x200     | 从驱动程序到 IddCx 的高频率游标相关调用 |
| 0x400     | 从内核到 IddCx 的调用 |
| 0x800     | 从 IddCx 调用到内核 |

0x0f4 的普通日志记录方案是一种很好的起点。 如果要查看每帧信息，0x1f4 是一个很好的起点。

##### <a name="flags-meaning-prior-to-windows-build-19041"></a>Windows build 19041 之前的标志含义

标志被视为一个级别，每个递增的级别都会添加一条新消息类型以及以前级别的所有消息。

| 标志级别值  | 捕获的消息类型 |
|:------------------:|-----------------------|
| 1                  | 未使用              |
| 2                  | 错误                |
| 3                  | 警告              |
| 4                  | 信息           |
| 5                  | “详细”               |

### <a name="decoding-iddcx-wpp-tracing"></a>解码 IddCx WPP 跟踪

与所有 WPP 跟踪一样，WPP 信息存储在*pdb*文件中，因此可以访问*pdb*，其中包含的信息需要解码。 从 Windows build 19560 开始，公共符号服务器上的*IddCx*包含解码 wpp 消息所需的 wpp 信息。 在 Windows 生成19560之前，公共符号服务器上的*IddCx* *不*包含必要的 WPP 信息以启用 wpp 解码。

任何标准 WPP 解码工具都可用于对消息进行解码和显示。

## <a name="debugging-iddcx-errors"></a>调试 IddCx 错误

开发间接显示驱动程序时，在 IddCx 检测到错误时获取其他信息通常很有用。 如上所述，你可以将 IddCx 配置为在 IddCx 检测到错误时进入调试器，但在最后几个跟踪消息中显示 IddCx 错误消息以了解错误的上下文也很有用。

使用上述部分，可以使用*logman.exe*启用 WPP 跟踪，并使用以下信息在故障点显示内核调试器中的内存中 WPP 缓冲区。

> [!NOTE]
>
> 为此，需要使用内核调试器（而非用户模式调试器）和 Windows build 19560 或更高版本，以便调试器获取包含 WPP 解码信息的*IddCx。*

在下面的示例中，间接显示驱动程序调用[**IddCxMonitorArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nf-iddcx-iddcxmonitorarrival)。 作为处理的一部分，IddCx 调用驱动程序的[**EvtIddCxMonitorQueryTargetModes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iddcx/nc-iddcx-evt_idd_cx_monitor_query_target_modes) DDI。 在此示例中，驱动程序返回的模式 DISPLAYCONFIG_VIDEO_SIGNAL_INFO。AdditionalSignalInfo 设置为零，这是无效的，将导致错误。

下面是所使用的调试程序命令列表：

| 命令                             | 含义  |
|-------------------------------------|----------|
| !wmitrace.bufdump                   | 列出所有日志记录缓冲区和名称，IddCx 是我们的名称，来自 logman.exe 命令行 |
| ！ wmitrace. logdump *LogBufferName*   | 对指定日志记录缓冲区的内容进行解码，并显示以下示例中的 IddCx |

下面是此示例的调试器输出：

```dbgcmd
0: kd> !wmitrace.bufdump
(WmiTrace) BufDump
    LoggerContext Array @ 0xFFFFE6055EB0AC40 [64 Elements]

 Logger Context  Number Available   Size    NPP Usage   PP Usage
================ ====== ========= ======== =========== ==========
ffffe6055ee6c800      4         2     4096       16384             Circular Kernel Context Logger
ffffe6055eaa8640      2         2    65536      131072             Eventlog-Security
ffffe6055eb83a00      2         1    65536      131072             DefenderApiLogger
ffffe6055ebb6a00      2         2    65536      131072             DefenderAuditLogger
ffffe6055eb74040      2         1    16384       32768             DiagLog
ffffe6055eb74640      4         2    65536      262144             Diagtrack-Listener
ffffe6055eaa8040      2         2    65536                 131072  EventLog-Application
ffffe6055eb7c040      2         1    65536      131072             EventLog-System
ffffe6055eb7c640      5         3    65536      327680             LwtNetLog
ffffe6055eb85040      4         2    65536      262144             Microsoft-Windows-Rdp-Graphics-RdpIdd-Trace
ffffe6055eb85680      8         6   131072     1048576             NetCore
ffffe6055eb89040      4         4     4096       16384             NtfsLog
ffffe6055eb89640      8         6   131072     1048576             RadioMgr
ffffe605683ef040      3         2     4096                  12288  WindowsUpdate_trace_log
ffffe6055eb8f640      2         2     2048        4096             UBPM
ffffe6055eb108c0      4         2    16384       65536             WdiContextLog
ffffe6055eb968c0      4         2    81920      327680             WiFiSession
ffffe60567e8a6c0      5         3     8192       40960             IddCx
ffffe605658379c0     10         9     3072       30720             umstartup
ffffe605659d4840     10         9   131072     1310720             SCM
ffffe605655af9c0      2         1    65536      131072             UserNotPresentTraceSession
ffffe605659d6840      2         1     4096        8192             COM
ffffe60565925080     10         8    20480      204800             Terminal-Services-LSM
ffffe60565956080     10         9    20480      204800             Terminal-Services-RCM
ffffe6055eba39c0     50        49     3072      153600             UserMgr
ffffe60567388280      2         2    32768       65536             WFP-IPsec Diagnostics
ffffe605678a3040      5         3     4096       20480             MpWppTracing-20200424-092923-00000003-ffffffff
ffffe60567e35080      2         1    65536      131072             ScreenOnPowerStudyTraceSession
ffffe605655e0a00      5         3     4096       20480             SHS-04242020-092951-7-7f
ffffe605692054c0      4         4     8192       32768             RdpIdd
ffffe60567f597c0      4         3    65536      262144             SgrmEtwSession
ffffe605678a9a00      4         4     8192       32768             DispBrok-DeskSrv
ffffe60569286680      4         4     8192       32768             DispBrok-Desk
ffffe605668026c0      4         4     8192       32768             DispBrok
================ ====== ========= ======== =========== ==========
                    195       159             6651904     143360

0: kd> !wmitrace.logdump IddCx
(WmiTrace) LogDump for Logger Id 0x13
Found Buffers: 5 Messages: 537, sorting entries
[1]0EF8.0CF0::04/24/2020-09:43:36.894 [cx][IddCx]DriverEntry: Enter
[1]0EF8.0CF0::04/24/2020-09:43:36.897 [cx][IddCx]?IddCxLibraryInitialize@@YAJXZ: Enter
[1]0EF8.0CF0::04/24/2020-09:43:36.897 [cx][IddCx]?IddCxLibraryInitialize@@YAJXZ: Exit
[1]0EF8.0CF0::04/24/2020-09:43:36.897 [cx][IddCx]DriverEntry: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.904 [cx][IddCx]?IddCxLibraryBindClient@@YAJPEAU_WDF_CLASS_BIND_INFO@@PEAPEAX@Z: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.904 [cx][IddCx]?IddCxLibraryBindClient@@YAJPEAU_WDF_CLASS_BIND_INFO@@PEAPEAX@Z: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplDeviceInitConfig: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplDeviceInitConfig: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplGetVersion: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.910 [cx][IddCx]IddCxImplGetVersion: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.911 [cx][IddCx]IddCxImplDeviceInitialize: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.912 [cx][IddCx]IddCxImplDeviceInitialize: New IddDevice 0x000001642F5E0770 created
[0]0EF8.0CF0::04/24/2020-09:43:36.912 [cx][IddCx]IddCxImplDeviceInitialize: Exit, status=STATUS_SUCCESS
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]IddCxImplAdapterInitAsync: Enter
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]?Init@IddAdapter@@QEAAXPEAUIDDCX_ADAPTER__@@PEAVIddDevice@@PEAUIDDCX_ADAPTER_CAPS@@@Z: New IddAdapter 0x000001642F5E77D0 created, API object 0xFFFFFE9BD0A18978, IddDevice 0x000001642F5E0770
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]?SendUserModeMessage@IddAdapter@@QEAAJIPEAXI0W4DXGK_IDD_ESCAPE_CODE@@PEAI@Z: Sending escape 0x0 to kernel
Unknown( 76): GUID=ac5ec775-ccdb-3c2c-6150-28b4eacacbc4 (No Format Information found).
[0]0EF8.0CF0::04/24/2020-09:43:36.917 [cx][IddCx]IddCxImplAdapterInitAsync: Exit, status=STATUS_SUCCESS
[0]0EF8.0558::04/24/2020-09:43:36.935 [cx][IddCx]?HandleKernelModeMessage@IddAdapter@@QEAAXIPEAXI0PEAI@Z: IddAdapter 0x000001642F5E77D0, processing command START_ADAPTER_COMPLETE from KMD
[0]0EF8.0558::04/24/2020-09:43:36.935 [cx][IddCx]?HandleKernelModeMessage@IddAdapter@@QEAAXIPEAXI0PEAI@Z: IddAdapter 0x000001642F5E77D0, Successful adapter start, Wddm Luid = 0xe6e90, Adapter caps 0x0, Session Id 0, Terminal Luid 0x0
[0]0EF8.0558::04/24/2020-09:43:36.935 [cx][IddCx]?HandleKernelModeMessage@IddAdapter@@QEAAXIPEAXI0PEAI@Z: Exit
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]<lambda_e42696d61f3ea0fd0d39fdb90d856b7b>::operator(): DDI: Calling EvtIddCxAdapterInitFinished DDI, IddAdapter 0xFFFFFE9BD0A18978
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorCreate: Enter
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorCreate: New IddMonitor 0x000001642F5EF720 created, API object 0xFFFFFE9BD0A11A38, IddAdapter 0x000001642F5E77D0
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorCreate: Exit, status=STATUS_SUCCESS
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]IddCxImplMonitorArrival: Enter
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Calling EvtIddCxParseMonitorDescriptio DDI to get mode count, Device 0x000001642F5E0770
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Return successfully from EvtIddCxParseMonitorDescriptio DDI to get mode count, mode count 23
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Calling EvtIddCxParseMonitorDescriptio DDI to get modes, Device 0x000001642F5E0770
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?ParseMonitorDescription@IddDevice@@QEAAXUIDDCX_MONITOR_DESCRIPTION@@AEAV?$vector@UIDDCX_MONITOR_MODE@@V?$allocator@UIDDCX_MONITOR_MODE@@@std@@@std@@AEAI@Z: DDI: Return successfully from EvtIddCxParseMonitorDescriptio DDI to get modes
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?AddMonitorModes@IddMonitor@@AEAAXAEAV?$vector@UTARGET_MONITOR_MODE@@V?$allocator@UTARGET_MONITOR_MODE@@@std@@@std@@@Z: IddMonitor 0x000001642F5EF720, parseMonitorDescription returned 23 modes.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Calling EvtIddCxMonitorQueryTargetModes DDI for mode count, IddMonitor 0x000001642F5EF720
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Return successfully from EvtIddCxMonitorQueryTargetModes DDI, mode count = 0x23
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Calling EvtIddCxMonitorQueryTargetModes DDI to get modes, IddMonitor 0x000001642F5EF720
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?QueryModes@IddMonitor@@AEAAXAEAV?$vector@UIDDCX_TARGET_MODE@@V?$allocator@UIDDCX_TARGET_MODE@@@std@@@std@@@Z: DDI: Return successfully from EvtIddCxMonitorQueryTargetModes DDI
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?StartWatchInternal@IddWatchdog@@AEAAXK@Z: IddWatchdog 0x000001642F5E77F0, still has pending watch not started by watchdog thread.
[0]0EF8.1588::04/24/2020-09:43:36.936 [cx][IddCx]?AddTargetModes@IddMonitor@@AEAAXAEAV?$vector@UTARGET_MONITOR_MODE@@V?$allocator@UTARGET_MONITOR_MODE@@@std@@@std@@@Z: IddMonitor 0x000001642F5EF720, queryTargetModes returned 23 modes.
[0]0EF8.1588::04/24/2020-09:43:55.341 [cx][IddCx] Throwing error (Status 0xc000000d(STATUS_INVALID_PARAMETER)) from function Validate in onecoreuap\windows\core\dxkernel\indirectdisplays\classext\cx\ddivalidation.cpp:412, Msg DISPLAYCONFIG_VIDEO_SIGNAL_INFO.AdditionalSignalInfo.vSyncFreqDivider cannot be zero for target mode
Total of 537 Messages from 5 Buffers

```

最后一行提供失败的原因。
