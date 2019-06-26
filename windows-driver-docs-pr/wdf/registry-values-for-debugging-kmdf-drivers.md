---
title: 用于调试 WDF 驱动程序（KMDF 和 UMDF）的注册表值
description: 本主题介绍 Windows 驱动程序框架 (WDF) 驱动程序可以设置的注册表值。 它适用于内核模式驱动程序框架 (KMDF) 驱动程序和用户模式驱动程序框架 (UMDF) 驱动程序从 UMDF 版本 2 开始。
ms.assetid: d54bdc6c-b409-4973-9b29-16967a4d83fb
keywords:
- 调试驱动程序 WDK KMDF，注册表值
- 调试驱动程序 WDK KMDF 注册表值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8900f1f77d8cbc2ad4dffbc35b887c8e9e07077d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376299"
---
# <a name="registry-values-for-debugging-wdf-drivers-kmdf-and-umdf"></a>用于调试 WDF 驱动程序（KMDF 和 UMDF）的注册表值


本指南介绍了 Windows 驱动程序框架 (WDF) 驱动程序可以设置的注册表值。 它适用于内核模式驱动程序框架 (KMDF) 驱动程序和用户模式驱动程序框架 (UMDF) 驱动程序从 UMDF 版本 2 开始。

以下注册表值下的驱动程序只能存在**参数\\Wdf**子项。 KMDF 驱动程序，此子项是否位于**HKEY\_本地\_机\\系统\\CurrentControlSet\\服务**，驱动程序的服务名称下。 UMDF 驱动程序，此子项是否位于**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\服务**下驱动程序的服务名称。 驱动程序的子项始终使用驱动程序的服务名称，即使该驱动程序二进制文件的文件名不同于服务名称。

<a href="" id="verifieron-----------------reg-dword-"></a>**VerifierOn** (**REG\_DWORD**)  
设置为非零值以启用[KMDF Verifier](using-kmdf-verifier.md)，广泛验证驱动程序的状态和函数参数。 应设置**VerifierOn**并**DbgBreakOnError**时你正在开发您的驱动程序。 使用[AddService 指令](../install/inf-addservice-directive.md)并[AddReg 指令](../install/inf-addreg-directive.md)例如 INF 文件的 Services 部分中设置这些值：

```
[xxx_Inst.NT.Services]
AddService = xxx,%SPSVCINST_ASSOCSERVICE%,xxx_Service_Inst

[xxx_Service_Inst]
ServiceType   = %SERVICE_KERNEL_DRIVER%
StartType     = %SERVICE_BOOT_START%
ErrorControl  = %SERVICE_ERROR_NORMAL%
LoadOrderGroup = "Base"
ServiceBinary = %12%\xxx.sys
AddReg         = KMDFVerifierAddReg

[KMDFVerifierAddReg]
HKR, Parameters\Wdf,VerifierOn,0x00010001,1
HKR, Parameters\Wdf,VerboseOn,0x00010001,1
HKR, Parameters\Wdf,DbgBreakOnError,0x00010001,1
```

<a href="" id="verifyon-----------------reg-dword-"></a>**VerifyOn** (**REG\_DWORD**)  
设置为非零值以启用[ **WDFVERIFY** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)中 Wdfassert.h，定义或设置为零表示禁用该宏的宏。 如果未设置 VerifierOn 值，VerifyOn 隐式设置为非零值。

<a href="" id="dbgbreakonerror--reg-dword-"></a>**DbgBreakOnError** (**REG\_DWORD**)  
如果设置为非零值，该框架进入调试器时驱动程序调用[ **WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)。 (如果**VerifierOn**值设置为，框架会中断到调试器，即使**DbgBreakOnError**值不存在。)请参阅上面的代码示例。

<a href="" id="dbgwaitforsignaltimeoutinsec--reg-dword-"></a>**DbgWaitForSignalTimeoutInSec** (**REG\_DWORD**)  
在 Windows 8 中，启动时**VerifierOn**并**DbgBreakOnError**设置为非零值，该驱动程序可以更改通过设置中断到调试器的默认超时期限**DbgWaitForSignalTimeoutInSec**。

此值是位于 framework 版本 1.11 及更高版本。

<a href="" id="verifierallocatefailcount-----------------reg-dword-"></a>**VerifierAllocateFailCount** (**REG\_DWORD**)  
如果设置为值*n*，并且如果**VerifierOn** ，则 framework 将失败，每次尝试为驱动程序的对象分配内存*第 n 个*分配。 此故障可帮助您测试您的驱动程序处理的内存不足情况。 例如，如果您设置**VerifierAllocateFailCount**为 2 之后的第二个分配, 每个内存分配会失败。 默认值为**VerifierAllocateFailCount**为 0xffffffff。 设置后**VerifierAllocateFailCount**，可以通过将其设置为 (DWORD)-1 将其关闭或完全删除值。

请注意，验证程序将您的驱动程序请求的分配和 framework 代表您的驱动程序请求的分配。 另请注意，为您的驱动程序可能会发生的分配数可以从一个版本的框架更改为下一步。

<a href="" id="trackhandles--reg-multi-sz-"></a>**TrackHandles** (**REG\_多\_SZ**)  
如果设置为一系列一个或多个类型名称的 framework 对象句柄，并且如果**VerifierOn** ，则框架跟踪对与指定句柄类型匹配的所有对象句柄的引用。 例如，如果句柄类型列表包含"WDFREQUEST WDFQUEUE"字符串，该框架将跟踪对所有请求的对象和队列对象的引用。 如果列表包含一个星号 ("\*")，该框架跟踪所有的对象句柄。

<a href="" id="verboseon-----------------reg-dword-"></a>**VerboseOn** (**REG\_DWORD**)  
如果设置为非零值，该框架的[事件记录器](using-the-framework-s-event-logger.md)记录其他信息可帮助你调试您的驱动程序，如条目或退出从内部代码路径。 仅在开发您的驱动程序时，应设置此值。 请参阅上面的代码示例。

<a href="" id="logpages--reg-dword-"></a>**LogPages** (**REG\_DWORD**)  
将设置为该框架将分配给其事件记录器的内存页面数。 如果未定义值，则框架将使用默认值为一页。 可以设置的最大值是 16 的计算机： 具有 4 千字节大小的内存页 （x86 和 amd64 处理器） 和 8 的计算机： 具有 8 千字节大小的内存页 （ia64 处理器）。 （操作系统可能会写入指定日志内容到如果大量的页面的崩溃转储文件。）使用[AddService 指令](../install/inf-addservice-directive.md)并[AddReg 指令](../install/inf-addreg-directive.md)若要将此值设置在 INF 文件中，按如下所示：

```
[xxx.NT.Services]
AddService = yyy, 2, zzz.AddService

[zzz.AddService]
DisplayName   = %aaa\bbb%
ServiceType   = 1
StartType     = 3
ErrorControl  = 1
ServiceBinary = %12%\ddd.SYS
AddReg         = eee.AddReg

[eee.AddReg]
HKR, Parameters\Wdf, LogPages,   0x00010001, 3 ; KMDF IFR size
```

<a href="" id="forcelogsinminidump--reg-dword-"></a>**ForceLogsInMiniDump** (**REG\_DWORD**)  
设置为非零值会导致崩溃转储文件中包括其事件记录器中的信息的框架。

<a href="" id="tracedelaytime--reg-dword-"></a>**TraceDelayTime** (**REG\_DWORD**)  
Microsoft Windows 2000，设置为非零值若要在初始化过程中引入延迟[WPP 软件跟踪](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)。 以毫秒为单位指定的值和有用的值为 1000 （1 秒）。 没有此延迟，可能会丢失 WPP 跟踪的第一个部分。

<a href="" id="enhancedverifieroptions-----------------reg-dword-"></a>**EnhancedVerifierOptions** (**REG\_DWORD**)  
此值包含的位图。 每个位表示用户可以通过设置位启用的其他验证程序选项。

*位值：*

**0x1**:如果设置，请验证工具将检查每个驱动程序的事件回调函数是否执行以下操作：

-   在相同的 IRQL 的调用返回。 如果值不同， [ **WDF\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation) bug 检查出现的错误代码为 0xE。

-   再返回，退出所有[临界区](https://docs.microsoft.com/windows-hardware/drivers/kernel/critical-regions-and-guarded-regions)其输入。 如果回调函数返回关键区域内输入，其[ **WDF\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation) bug 检查出现的错误代码为 0xF。

**0x10000**:如果设置，并且如果该驱动程序已启用[保证向前推进](guaranteeing-forward-progress-of-i-o-operations.md)I/O 队列，该框架模拟内存不足的情况下为每个队列的 I/O 请求。

**0x20000**:如果设置，并且如果该驱动程序已启用的 I/O 队列保证向前推进，框架将模拟某些随机选择的 I/O 请求的内存不足的情况。

此值是可用在 framework 版本 1.9 及更高版本。

<a href="" id="verifydownlevel--reg-dword-"></a>**VerifyDownLevel** (**REG\_DWORD**)  
如果设置为非零值，和框架的验证程序如果驱动程序使用早于当前版本的 framework 版本生成，包括驱动程序已生成后已添加的测试。 如果此值不存在，或者设置为零，框架的验证程序包括仅存在于该驱动程序生成时的测试。

例如，如果您的驱动程序生成为版本 1.7 的框架，并且计算机上安装的 framework 版本 1.9，设置**VerifyDownLevel**不为零将导致的验证程序，包括已添加到的测试当您的驱动程序运行时的验证程序 1.9 版中。

此值是可用在 framework 版本 1.9 及更高版本。

## <a name="kmdf"></a>KMDF


将以下注册表值下 KMDF 驱动程序，只能存在**HKLM\\系统\\CurrentControlSet\\控制\\Wdf\\Kmdf\\诊断**注册表项。 将以下注册表值下 UMDF 驱动程序，只能存在**HKLM\\系统\\CurrentControlSet\\控制\\Wdf\\Umdf\\诊断**注册表项。 该驱动程序可能需要创建可选**诊断**子项。

<a href="" id="dbgprinton--reg-dword-"></a>**DbgPrintOn** (**REG\_DWORD**)  
如果设置为非零值，框架的加载程序将发送各种消息到内核调试程序时它是加载驱动程序并将其绑定到版本的框架库，或卸载驱动程序时。

## <a name="umdf"></a>UMDF


此外可以设置以下注册表值**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\服务\\{193a1820-d9ac-4997-8c55-be817523f6aa}** 。 这些值会影响系统上的所有 UMDF 驱动程序。

<a href="" id="hostprocessdbgbreakonstart--reg-dword-"></a>**HostProcessDbgBreakOnStart** (**REG\_DWORD**)  
在数秒内包含的延迟值。 在指定的延迟期间，主机进程中查找用户模式下调试程序一次第二个并且如果其中一个连接中的换行符。 如果在此时间段和中的高位未附加用户模式调试器**HostProcessDbgBreakOnStart**设置 (0x80000000)，可以一次尝试进入内核模式调试程序的框架。 例如：

|            |                                                                                                                                                                                                                  |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ReplTest1      | 结果                                                                                                                                                                                                           |
| 0x00000004 | 框架尝试连接到用户模式下调试程序一次一种为 4 秒。 框架永远不会尝试连接到内核模式调试程序。                                                       |
| 0x80000000 | 该框架可以一次尝试连接到用户模式下调试程序。 如果用户模式下调试器未附加，框架将尝试连接到内核模式调试程序。                                |
| 0x80000004 | 框架尝试连接到用户模式下调试程序一次一种为 4 秒。 如果在 4 秒内未附加用户模式下调试程序，该框架将尝试连接到内核模式调试程序。 |

 

<a href="" id="hostprocessdbgbreakondriverload--reg-dword-"></a>**HostProcessDbgBreakOnDriverLoad** (**REG\_DWORD**)  
在数秒内包含的延迟值。 导致 WUDFHost 延迟指定的加载该驱动程序之后的秒数。 行为**HostProcessDbgBreakOnDriverLoad**在其他方面所述的相同**HostProcessDbgBreakOnStart**。

指定**HostProcessDbgBreakOnStart**或**HostProcessDbgBreakOnDriverLoad**会导致禁用其他 UMDF 超时 （例如，插操作） 框架。 这意味着，如果您的驱动程序导致过多的超时，使用这些值可能会导致您的目标上导致严重故障的驱动程序。

此外可以通过使用 WDK 中包含 WDF 验证程序工具 (WdfVerifier.exe) 来设置这些注册表值。 在 UMDF 驱动程序中使用此工具的信息，请参阅[WDF 验证程序与管理 UMDF 验证程序的设置](https://docs.microsoft.com/windows-hardware/drivers/devtest/global-wdf-settings-tab)。

以下附加属性值都位于**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\DebugMode**:

<a href="" id="debugmodeflags--reg-dword-"></a>**DebugModeFlags** (**REG\_DWORD**)  
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>启用调试模式。 此设置将禁用自动重新启动功能中所述<a href="using-device-pooling-in-umdf-drivers.md" data-raw-source="[Using Device Pooling in UMDF Drivers](using-device-pooling-in-umdf-drivers.md)">UMDF 驱动程序中使用设备池</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>禁用设备池。 有关设备池的详细信息，请参阅<a href="using-device-pooling-in-umdf-drivers.md" data-raw-source="[Using Device Pooling in UMDF Drivers](using-device-pooling-in-umdf-drivers.md)">UMDF 驱动程序中使用设备池</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>禁用超时。</p></td>
</tr>
</tbody>
</table>

 

当在 Microsoft Visual Studio 中使用 F5 选项时，所有三个标记为已部署的驱动程序设置。

<a href="" id="debugmodebinaries--reg-sz-"></a>**DebugModeBinaries** (**REG\_多\_SZ**)  
此值指定为在调试模式下加载的驱动程序二进制文件的名称。 若要启用调试模式下为 X.DLL、 Y.DLL 和 Z.DLL 的驱动程序二进制文件，例如，此值将设置为*X.DLL\\0 Y。DLL\\0Z.DLL\\0\\0*。

此外可以设置以下值**HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**:

<a href="" id="hostfailkddebugbreak--reg-dword-"></a>**HostFailKdDebugBreak** (**REG\_DWORD**)  
如果此值为非零值且内核调试程序连接到计算机，该发送程序在主机进程终止前强行进入内核调试器。 **HostFailKdDebugBreak** Windows 7 和更早的操作系统中默认处于禁用状态。 在 Windows 8 中，启动**HostFailKdDebugBreak**默认情况下启用。

如果主机进程 （例如，非 UMDF 组件或由于未经处理的异常） 的意外的终止，该发送程序也会中断到内核调试程序。 如果有多个设备堆栈被终止的主机进程中放入池中，该发送程序进入调试器多次，一次为在主机进程中加载每个设备堆栈。

对 UMDF 注册表值才能生效的更改，必须重新启动计算机。

 

 





