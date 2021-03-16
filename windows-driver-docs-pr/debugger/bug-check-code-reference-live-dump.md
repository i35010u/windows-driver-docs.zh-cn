---
title: 内核实时转储代码引用
description: 本部分包含常见内核实时转储的说明，并介绍它们与传统 bug 检查的不同之处。
ms.date: 03/10/2021
ms.localizationpriority: high
ms.openlocfilehash: b4ac4e518a63288befddbc79e972a0ba5cb08034
ms.sourcegitcommit: 47cd14eb928aee3a3368d9d1d92a7047b30eac55
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/11/2021
ms.locfileid: "103022980"
---
# <a name="kernel-live-dump-code-reference"></a>内核实时转储代码引用

本部分包含可能会出现的常见内核实时转储代码的说明。 实时转储会不重置 OS，但允许在操作系统可继续的异常情况下捕获内存信息。

> [!NOTE]
> 本主题面向程序员。 如果你是一个客户，你的系统显示了带有 bug 检查代码的蓝屏，请参阅[蓝屏错误疑难解答](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。

## <a name="kernel-live-dump-compared-to-bug-check"></a>内核实时转储与 bug 检查的比较

使用传统 bug 检查时，PC 将重置，并且用户的工作将中断。 内核实时转储的目标是收集数据以对异常情况进行故障排除，但允许 OS 继续操作。 与“非致命”但影响严重的失败和挂起的 bug 检查相比，这可以减少停机时间。 如果可以将 OS 恢复到已知的良好状态，则使用内核实时转储。 例如，子系统的硬件重置（如视频/显示、USB3 或 Wi-Fi）可以允许这些系统恢复到已知的良好状态，同时对用户的影响降到最低。

内核实时转储创建内核内存的一致性快照，并将其保存到转储文件以供将来分析。 为了最大限度地减少对性能的影响，使用内存复制技术在短时间内创建转储文件。 此外，还会限制实时转储的收集，从而最大程度地减少对用户的影响。

内核实时转储适用于一类问题，即需要花费很长时间，但并未出现任何技术故障的问题。 启动操作时，可以初始化监视器计时器。 如果监视器在预期时间内在操作完成之前过期，则可以执行系统的实时转储。 然后，可以通过遍历该操作的调用堆栈和相关等待链来分析转储，以调查它未在预期的时间范围内完成的原因。

当某些操作失败，代码所有者记录失败的原因并能确定原因时，系统日志很有用。 使用监视器计时器的实时转储尝试捕获预期和记录外的故障路径。 但与每个故障一样，系统日志可能会标识其他问题，这些原因可能提供有关失败的特定根本原因的线索。

## <a name="kernel-live-dump-file-contents"></a>内核实时转储文件内容

与常规转储文件类似，实时转储文件可能包含（具有次要数据）的小型转储以及完整的内核转储，后者中也可能包含与活动转储类似的用户模式内存。 有关转储文件内容的常规信息，请参阅[多种内核模式转储文件](varieties-of-kernel-mode-dump-files.md)。 某些实时转储只会尝试捕获小型转储，因为它们旨在捕获特定的硬件相关数据，而另一些则可能尝试捕获更大的内核实时转储。

为了性能、文件大小以及转储捕获的可靠性，某些信息不包括在内，例如来自备用列表和文件缓存的页面。

实时转储文件通常包含内存页面，例如：

- KdDebuggerBlock
- 加载的模块列表

对于每个处理器，内核转储中会捕获以下信息：

- KiProcessorBlock
- PRCBs
- 当前堆栈
- 当前页面目录表
- KI_USER_SHARED_DATA
- NTOS 内核映像
- HAL 映像

内核转储中的其他信息可能包括：

- 线程/内存状态
- 内存中日志记录

某些实时转储可能包含用户模式进程页面。

某些实时转储可能包含其他特定于域的数据，例如 USB 故障种特定于 USB 的数据。

## <a name="partial-kernel-live-dump-file"></a>部分内核实时转储文件

当实时转储无法可靠地捕获所有预期的内存页面时，可能会生成部分内核实时转储文件。 将通过捕获包含在其他页面之前生成有效转储所需的重要数据的页面，筛选在部分转储中捕获的信息并确定其优先级。 例如，当实时转储包括用户页面时，内核页面优先于用户页面。  在某些情况下，没有足够的资源可用于捕获所有预期的可选内存页面，因此转储文件中可能缺少内存。 WinDbg 调试器仍应识别转储文件，但在尝试转储内存时可能会显示错误。  如果调试器在尝试转储位于某个地址的内存时显示错误，则可以使用 [!pte](-pte.md) 扩展来检查地址的 PTE 是否有效。 这可以帮助确定是内存地址确实无效，还是页面有效只是在转储文件中不可用。

## <a name="analyzing-live-dump-files"></a>分析实时转储文件

发生实时转储时，可以使用用于其他内存转储文件的技术来分析转储文件。 若要了解故障期间的内存内容，需要了解处理器内存寄存器和程序集编程。

有关详细信息，请参阅：

- [使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

- [!analyze](-analyze.md)

- [处理器体系结构](processor-architecture.md)

## <a name="using-windbg-to-display-live-dump-stop-code-information"></a>使用 WinDbg 显示实时转储终止代码信息

如果此主题中没有某个实时转储代码的说明信息，请在 Windows 调试程序 (WinDbg) 中使用以下语法（内核模式）和 [ **!analyze**](-analyze.md) 扩展，并将 `<code>` 替换为某个 Bug 检查代码：

`!analyze -show <code>`

输入此命令会使 WinDbg 显示指定的实时转储代码的相关信息。 如果默认数字基数不是 16，则为 `<code>` 添加前缀 **0x**。

向 !analyze 命令提供实时转储代码参数，以显示任何可用的参数信息。 例如，若要显示有关参数 1 值为 0x3003 的 [Bug 检查 0x144 BUGCODE_USB3_DRIVER](bug-check-0x144--bugcode-usb3-driver.md) 的信息，请使用 `!analyze -show 0x144 0x3003`，如下所示。  

```dbgcmd
0: kd> !analyze -show 0x144 0x3003
BUGCODE_USB3_DRIVER (144)
This bugcheck usually happens when the USB3 core stack detects an invalid
operation being performed by a USB client. This bugcheck may also occur
due to hardware failure on a USB Boot Device.
Arguments:
Arg1: 0000000000003003, USB3_WER_BUGCODE_USBHUB3_DEVICE_ENUMERATION_FAILURE
    A USB device failed enumeration.
Arg2: 0000000000000000, USBHUB3_LIVEDUMP_CONTEXT
Arg3: 0000000000000000, 0
Arg4: 0000000000000000, 0
```

若要下载 WinDbg，请参阅[下载 Windows调试工具](debugger-download-tools.md)。 若要了解有关 WinDbg 开发工具的详细信息，请参阅 [Windows 调试入门](getting-started-with-windows-debugging.md)。

## <a name="live-dump-file-locations"></a>实时转储文件位置

实时转储默认存储在“C:\WINDOWS\LiveKernelReports”目录中。

完全转储：`%systemroot%\LiveKernelReports\*.dmp`

小型转储：`%systemroot%\LiveKernelReports\<ComponentName>\*.dmp`

目录结构用于存储不同组件的实时转储。

```dos
NDIS
PDCRevocation
PoW32kWatchdog
USBHUB3
WATCHDOG
```

## <a name="live-dump-registry-keys"></a>实时转储注册表项

有关系统生成的实时内核报表的配置选项的详细信息，请参阅 [WER 设置](/windows/win32/wer/wer-settings#crashcontrolfulllivekernelreports-subkey)。

## <a name="use-powershell-to-manually-trigger-a-live-dump"></a>使用 PowerShell 手动触发实时转储

1. 打开和管理员 PowerShell 提示符。

2. 使用 [Get-StorageSubSystem](/powershell/module/storage/get-storagesubsystem) PowerShell 命令获取 StorageSubSystem 易记名称。

```powershell
 C:\> Get-StorageSubSystem
 FriendlyName                     HealthStatus OperationalStatus
 ------------                     ------------ -----------------
 Windows Storage on 10-2411-PC    Healthy      OK
```

3. 使用 Get-StorageDiagnosticInfo 生成上述子系统的实时转储（以及其他诊断日志）。 有关详细信息，请参阅 [Get-StorageDiagnosticInfo](/powershell/module/storage/get-storagediagnosticinfo)。

```powershell
 C:\> Get-StorageDiagnosticInfo -StorageSubSystemFriendlyName "Windows Storage on 10-2411-PC" -IncludeLiveDump -DestinationPath C:\destinationfolder
```

4. 输出将指示正在生成请求的信息。

```powershell
Gathering storage subsystem diagnostic information                                                                         
Running                                                                                                                 
[oooooooooooo                                                                                              ] 
```

5. 转储将位于 `[DestinationPath]\localhost` 内。

```powershell
 C:\> dir C:\destinationfolder\localhost\*.dmp
   Directory: C:\destinationfolder\localhost
 Mode                LastWriteTime         Length Name
 ----                -------------         ------ ----
 -a----         5/5/2016   1:08 PM      867135488 LiveDump.dmp
```

6. 使用调试程序在转储文件上运行 [!analyze](-analyze.md) 将指示这是 [LIVE_SYSTEM_DUMP (161)](bug-check-0x161--live-system-dump.md) 的实时转储代码。

## <a name="kernel-live-dump-codes"></a>内核实时转储代码

下表提供了内核实时转储代码的链接。

| 代码       | 名称                                                                                                                                              |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x000000AB | [**SESSION\_HAS\_VALID\_POOL\_ON\_EXIT**](bug-check-0xab--session-has-valid-pool-on-exit.md)                                                      |
| 0x00000117 | [**VIDEO\_TDR\_TIMEOUT\_DETECTED**](bug-check-0x117---video-tdr-timeout-detected.md)                                                              |
| 0x00000141 | [**VIDEO\_ENGINE\_TIMEOUT\_DETECTED**](bug-check-0x141---video-engine-timeout-detected.md)                                                        |
| 0x00000142 | [**VIDEO\_TDR\_APPLICATION\_BLOCKED**](bug-check-0x142--video-tdr-application-blocked.md)                                                         |
| 0x00000156 | [**WINSOCK\_DETECTED\_HUNG\_CLOSESOCKET\_LIVEDUMP**](bug-check-0x156--winsock-detected-hung-closesocket-livedump.md)                              |
| 0x0000015C | [**PDC\_WATCHDOG\_TIMEOUT\_LIVEDUMP**](bug-check-0x15c--pdc-watchdog-timeout-livedump.md)                                                         |  
| 0x0000015D | [**SOC\_SUBSYSTEM\_FAILURE\_LIVEDUMP**](bug-check-0x15d-soc-subsystem-failure-livedump.md)                                                        |
| 0x0000015E | [**BUGCODE\_NDIS\_DRIVER\_LIVE\_DUMP**](bug-check-0x15e-bugcode-ndis-driver-live-dump.md)                                                         |
| 0x0000015F | [**CONNECTED\_STANDBY\_WATCHDOG\_TIMEOUT\_LIVEDUMP**](bug-check-0x15f--connected-standby-watchdog-timeout-livedump.md)                            |
| 0x00000161 | [**LIVE\_SYSTEM\_DUMP**](bug-check-0x161--live-system-dump.md)                                                                                    |
| 0x00000165 | [**CLUSTER\_CSV\_STATUS\_IO\_TIMEOUT\_LIVEDUMP**](bug-check-0x165--cluster-csv-staus-io-timeout-livedump.md)                                      |
| 0x00000166 | [**CLUSTER\_RESOURCE\_CALL\_TIMEOUT\_LIVEDUMP**](bug-check-0x166--cluster-resource-call-timeout-livedump.md)                                      |
| 0x00000167 | [**CLUSTER\_CSV\_SNAPSHOT\_DEVICE\_INFO\_TIMEOUT\_LIVEDUMP**](bug-check-0x167--cluster-csv-snapshot-device-info-timeout-livedump.md)              |
| 0x00000168 | [**CLUSTER\_CSV\_STATE\_TRANSITION\_TIMEOUT\_LIVEDUMP**](bug-check-0x168--cluster-csv-state-transition-timeout-livedump.md)                       |   
| 0x00000169 | [**CLUSTER\_CSV\_VOLUME\_ARRIVAL\_LIVEDUMP**](bug-check-0x169--cluster-csv-volume-arival-livedump.md)                                             |      
| 0x0000016A | [**CLUSTER\_CSV\_VOLUME\_REMOVAL\_LIVEDUMP**](bug-check-0x16a--cluster-csv-volume-removal-livedump.md)                                            |    
| 0x0000016B | [**CLUSTER\_CSV\_CLUSTER\_WATCHDOG\_LIVEDUMP**](bug-check-0x16b--cluster-csv-cluster-watchdog-livedump.md)                                        |   
| 0x0000016F | [**CLUSTER\_CSV\_STATE\_TRANSITION\_INTERVAL\_TIMEOUT\_LIVEDUMP**](bug-check-0x16f--cluster-csv-state-transistion-interval-livedump.md)           |
| 0x00000175 | [**PREVIOUS\_FATAL\_ABNORMAL\_RESET\_ERROR**](bug-check-0x175--previous-fatal-abnormal-reset-error.md)                                            |
| 0x00000179 | [**CLUSTER\_CLUSPORT\_STATUS\_IO\_TIMEOUT\_LIVEDUMP**](bug-check-0x179--cluster-clusport-status-io-timeout-livedump.md)                           |
| 0x0000017C | [**PDC\_LOCK\_WATCHDOG\_LIVEDUMP**](bug-check-0x17c--pdc-lock-watchdog-livedump.md)                                                               | 
| 0x0000017D | [**PDC\_UNEXPECTED\_REVOCATION\_LIVEDUMP**](bug-check-0x17d-unexpected-revocation-livedump.md)                                                    | 
| 0x00000187 | [**VIDEO\_DWMINIT\_TIMEOUT\_FALLBACK\_BDD**](bug-check-0x187--video-dwminit-timeout-fallback-bdd.md)                                              |
| 0x00000188 | [**CLUSTER\_CSVFS\_LIVEDUMP**](bug-check-0x188--cluster-csvfs-livedump.md)                                                                        |
| 0x00000190 | [**WIN32K\_CRITICAL\_FAILURE\_LIVEDUMP**](bug-check-0x190--win32k-critical-failure-livedump.md)                                                   |
| 0x00000193 | [**VIDEO\_DXGKRNL\_LIVEDUMP**](bug-check-0x192--video-dxgkrnl-livedump.md)                                                                        |
| 0x00000195 | [**SMB\_SERVER\_LIVEDUMP**](bug-check-0x195--smb-server-livedump.md)                                                                              |
| 0x00000198 | [**UFX\_LIVEDUMP**](bug-check-0x198--ufx-livedump.md)                                                                                             |
| 0x0000019D | [**CLUSTER\_SVHDX\_LIVEDUMP**](bug-check-0x19d--cluster-svhdx-livedump.md)                                                                        |
| 0x000001A1 | [**WIN32K\_CALLOUT\_WATCHDOG\_LIVEDUMP**](bug-check-0x1a1--win32k-callout-watchdog-livedump.md)                                                   |
| 0x000001A3 | [**CALL\_HAS\_NOT\_RETURNED\_WATCHDOG\_TIMEOUT\_LIVEDUMP**](bug-check-0x1a3--call-has-not-returned-watchdog-timeout-livedump.md)                  |
| 0x000001A4 | [**DRIPS\_SW\_HW\_DIVERGENCE\_LIVEDUMP**](bug-check-0x1a4--drips-sw-hw-divergence-livedump.md)                                                    |
| 0x000001A5 | [**USB\_DRIPS\_BLOCKER\_SURPRISE\_REMOVAL\_LIVEDUMP**](bug-check-0x1a5--usb-drips-blocker-surprise-removal-livedump.md)                           |
| 0x000001A6 | [**BLUETOOTH\_ERROR\_RECOVERY\_LIVEDUMP**](bug-check-0x1a6--bluetooth-error-recovery-livedump.md)                                                 |
| 0x000001A7 | [**SMB\_REDIRECTOR\_LIVEDUMP**](bug-check-0x1A7--smb-redirector-livedump.md)                                                                      |
| 0x000001A8 | [**VIDEO\_DXGKRNL\_BLACK\_SCREEN\_LIVEDUMP**](bug-check-0x1a8--video-dxgkrnl-black-screen-livedump.md)                                            |
| 0x000001B0 | [**VIDEO_MINIPORT_FAILED_LIVEDUMP**](bug-check-0x1b0--video-miniport-failed-livedump.md)                                                          |
| 0x000001B8 | [**VIDEO_MINIPORT_BLACK_SCREEN_LIVEDUMP**](bug-check-0x1b8--video-miniport-black-screen-livedump.md)                                              |
| 0x000001C4 | [**DRIVER\_VERIFIER\_DETECTED\_VIOLATION\_LIVEDUMP**](bug-check-0x1c4--driver-verifier-detected-violation-livedump.md)                            |
| 0x000001C5 | [**IO\_THREADPOOL\_DEADLOCK\_LIVEDUMP**](bug-check-0x1c5--io-threadpool-deadlock-livedump.md)                                                     |
| 0x000001C9 | [**USER\_MODE\_HEALTH\_MONITOR\_LIVEDUMP**](bug-check-0x1c9--user-mode-health-monitor-livedump.md)                                                |
| 0x000001CC | [**EXRESOURCE_TIMEOUT_LIVEDUMP**](bug-check-0x1cc--exresource-timeout-livedump.md)                                                                |
| 0x000001D1 | [**TELEMETRY\_ASSERTS\_LIVEDUMP**](bug-check-0x1d1--telemetry-asserts-livedump.md)                                                                |
| 0x000001D4 | [**UCMUCSI\_LIVEDUMP**](bug-check-0x1d4--ucmusci-livedump.md)                                                                                     |

这些停止代码可用于实时转储或设备 bug 检查。

| 代码       | 名称                                                                            |
|------------|---------------------------------------------------------------------------------|
| 0x00000124 | [**WHEA\_UNCORRECTABLE\_ERROR**](bug-check-0x124---whea-uncorrectable-error.md) |
| 0x00000144 | [**BUGCODE\_USB3\_DRIVER**](bug-check-0x144--bugcode-usb3-driver.md)            |
| 0x00000164 | [**WIN32K\_CRITICAL\_FAILURE**](bug-check-0x164--win32k-critical-failure.md)    |
