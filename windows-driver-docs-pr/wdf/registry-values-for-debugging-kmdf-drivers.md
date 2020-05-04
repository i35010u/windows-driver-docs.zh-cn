---
title: 用于调试 WDF 驱动程序（KMDF 和 UMDF）的注册表值
description: 本主题介绍 Windows 驱动程序框架（WDF）驱动程序可以设置的注册表值。 它适用于从 UMDF 版本2开始的内核模式驱动程序框架（KMDF）驱动程序和用户模式驱动程序框架（UMDF）驱动程序。
ms.assetid: d54bdc6c-b409-4973-9b29-16967a4d83fb
keywords:
- 调试驱动程序 WDK KMDF，注册表值
- 调试驱动程序的注册表值 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8abcfbb2651934f691055f35a9a3cb6a7e3a2f00
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223087"
---
# <a name="registry-values-for-debugging-wdf-drivers-kmdf-and-umdf"></a>用于调试 WDF 驱动程序（KMDF 和 UMDF）的注册表值


本文介绍 Windows 驱动程序框架（WDF）驱动程序可以设置的注册表值。 它适用于从 UMDF 版本2开始的内核模式驱动程序框架（KMDF）驱动程序和用户模式驱动程序框架（UMDF）驱动程序。

驱动程序的**参数\\Wdf**子项下可以存在以下注册表值。 对于 KMDF 驱动程序，此子项位于驱动程序的服务名称下的**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services**中。 对于 UMDF 驱动程序，此子项位于该驱动程序的服务名称下的**HKLM\\SOFTWARE\\\\Microsoft Windows\\NT CurrentVersion\\WUDF\\Services**中。 驱动程序的子项始终使用驱动程序的服务名称，即使驱动程序二进制文件的文件名不同于服务名称也是如此。

## <a name="verifieron"></a>VerifierOn

*REG\_DWORD*

如果设置为非零值，则启用[KMDF 验证](using-kmdf-verifier.md)程序，该验证器会广泛验证驱动程序的状态和函数参数。 开发驱动程序时，应设置**VerifierOn**和**DbgBreakOnError** 。 使用[AddService 指令](../install/inf-addservice-directive.md)和[ADDREG 指令](../install/inf-addreg-directive.md)在 INF 文件的 Services 节中设置这些值，例如：

```inf
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

## <a name="verifyon"></a>VerifyOn

*REG\_DWORD*

如果设置为非零值，则启用在 Wdfassert 中定义的[**WDFVERIFY**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)宏，或设置为零以禁用宏。 如果设置了 VerifierOn 值，则 VerifyOn 将隐式设置为非零值。

## <a name="dbgbreakonerror"></a>DbgBreakOnError

*REG\_DWORD*

如果设置为非零值，则当驱动程序调用[**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)时，框架会中断到调试器。 （如果设置了**VerifierOn**值，则即使**DbgBreakOnError**值不存在，框架也会中断调试器。）请参阅上面的代码示例。

## <a name="dbgwaitforsignaltimeoutinsec"></a>DbgWaitForSignalTimeoutInSec

*REG\_DWORD，framework 版本1.11 及更高版本*

从 Windows 8 开始，当**VerifierOn**和**DbgBreakOnError**设置为非零值时，驱动程序可以通过设置**DbgWaitForSignalTimeoutInSec**更改用于中断到调试器的默认超时时间。


## <a name="verifierallocatefailcount"></a>VerifierAllocateFailCount

*REG\_DWORD*

如果设置为值*n*，并且如果设置了**VerifierOn** ，则在第*n*个分配后，框架将无法每次尝试为驱动程序的对象分配内存。 此故障有助于测试驱动程序对内存不足情况的处理。 例如，如果将**VerifierAllocateFailCount**设置为2，则在第二次分配后的每个内存分配都将失败。 **VerifierAllocateFailCount**的默认值为0xffffffff。 设置**VerifierAllocateFailCount**后，可以通过将其设置为（DWORD）-1 或完全删除该值来将其关闭。

请注意，该验证器会计算驱动程序请求的分配数和框架代表驱动程序请求的分配数。 另请注意，可能会对驱动程序进行的分配数从框架的一个版本更改为下一个版本。

## <a name="trackhandles"></a>TrackHandles

*REG\_多\_SZ*

如果设置为框架对象句柄的一个或多个类型名称的列表，并且如果设置了**VerifierOn** ，则框架将跟踪与指定的句柄类型匹配的所有对象句柄的引用。 例如，如果 "句柄类型" 列表包含 "WDFREQUEST WDFQUEUE" 字符串，则框架将跟踪对所有请求对象和队列对象的引用。 如果列表包含星号（"\*"），则框架将跟踪所有对象句柄。

## <a name="verboseon"></a>VerboseOn

*REG\_DWORD*

如果设置为非零值，框架的[事件记录器](using-the-framework-s-event-logger.md)将记录有助于调试驱动程序的其他信息，例如，条目进入或退出内部代码路径。 只有在开发驱动程序时，才应设置此值。 请参阅上面的代码示例。

## <a name="logpages"></a>LogPages

*REG\_DWORD*

设置为框架分配给其事件记录器的内存页数。 如果未定义此值，则框架将使用一个页面的默认值。 对于具有 4 kb 大小的内存页（x86 和 amd64 处理器）的计算机，可以设置的最大值为16，对于具有 8 kb 大小的内存页（ia64 处理器）的计算机，可以设置的最大值为8。 （如果指定了大量页面，操作系统可能无法将日志内容写入故障转储文件。）使用[AddService 指令](../install/inf-addservice-directive.md)和[ADDREG 指令](../install/inf-addreg-directive.md)在 INF 文件中设置此值，如下所示：

```inf
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

## <a name="forcelogsinminidump"></a>ForceLogsInMiniDump

*REG\_DWORD*

设置为一个非零值，以使框架在崩溃转储文件中包含其事件记录器中的信息。


## <a name="enhancedverifieroptions"></a>EnhancedVerifierOptions

*REG\_DWORD，framework 版本1.9 及更高版本*

此值包含位图。 每个位都表示一个附加的验证程序选项，用户可以通过设置该选项来启用该选项。

*位值：*

**0x1**：如果设置，验证程序将检查每个驱动程序的事件回调函数是否执行以下操作：

-   返回与调用该方法的 IRQL 相同的。 如果这些值不同，则会[**发生\_WDF 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)bug 检查，并出现错误代码0xE。

-   返回之前，会退出其输入的所有[关键区域](https://docs.microsoft.com/windows-hardware/drivers/kernel/critical-regions-and-guarded-regions)。 如果回调函数在它所输入的关键区域内返回，则[**出现\_WDF 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)bug 检查，并出现错误代码0xF。

**0x10000**：如果已设置，并且如果驱动程序已为 i/o 队列启用了[保证前进进度](guaranteeing-forward-progress-of-i-o-operations.md)，则该框架将模拟每个队列的 i/o 请求的低内存情况。

**0x20000**：如果已设置，并且如果驱动程序已为 i/o 队列启用了保证前进进度，则该框架将模拟某些随机选择的 i/o 请求的低内存情况。


## <a name="verifydownlevel"></a>VerifyDownLevel

*REG\_DWORD，framework 版本1.9 及更高版本*

如果设置为非零值，并且该驱动程序是使用比当前版本旧的 framework 版本生成的，则该框架的验证程序将包含在生成驱动程序之后添加的测试。 如果此值不存在或设置为零，则框架的验证器将仅包含生成驱动程序时存在的测试。

例如，如果你的驱动程序是用 framework 1.7 版构建的，并且如果计算机上安装了 framework 版本1.9，则将**VerifyDownLevel**设置为非零会导致该验证程序包含在你的驱动程序运行时添加到 verifier 版本1.9 的测试。


## <a name="dbgprinton"></a>DbgPrintOn

*REG\_DWORD*

如果设置为非零值，则框架的加载程序将向内核调试器发送各种消息，同时加载驱动程序并将其绑定到框架库版本，或者在卸载驱动程序时。

对于 KMDF 驱动程序，请在**\\HKLM\\SYSTEM CurrentControlSet\\Control\\Wdf\\KMDF\\Diagnostics**注册表项下设置此值。 对于 UMDF 驱动程序，请在**\\HKLM\\系统 CurrentControlSet\\控制\\Wdf\\UMDF\\诊断**注册表项下设置此值。 驱动程序可能需要创建可选的**诊断**子项。


你还可以在**HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\{193a1820-d9ac-4997-8c55-be817523f6aa}** 中设置以下注册表值。 这些值会影响系统上的所有 UMDF 驱动程序。

## <a name="hostprocessdbgbreakonstart"></a>HostProcessDbgBreakOnStart

*REG\_DWORD，仅 UMDF*

包含延迟值（以秒为单位）。 在指定的延迟期间，主机进程每秒查找用户模式调试器一次，并在连接的情况下中断。 如果在这段时间内未附加用户模式的调试程序，并且**HostProcessDbgBreakOnStart**中的高位（0x80000000）已设置，则该框架将进行一次尝试进入内核模式调试器。 例如：

|“值”|结果|
|--- |--- |
|0x00000004|框架每秒尝试连接到用户模式调试器一次，4秒。 框架从不尝试连接到内核模式调试器。|
|0x80000000|该框架将创建一次尝试连接到用户模式调试器。 如果未附加用户模式调试器，框架将尝试连接到内核模式调试器。|
|0x80000004|框架每秒尝试连接到用户模式调试器一次，4秒。 如果未在4秒内附加用户模式调试器，框架将尝试连接到内核模式调试器。|


## <a name="hostprocessdbgbreakondriverload"></a>HostProcessDbgBreakOnDriverLoad

*REG\_DWORD，仅 UMDF*

包含延迟值（以秒为单位）。 导致 WUDFHost 在加载驱动程序后延迟指定的秒数。 否则， **HostProcessDbgBreakOnDriverLoad**的行为与为**HostProcessDbgBreakOnStart**所述的行为相同。

指定**HostProcessDbgBreakOnStart**或**HostProcessDbgBreakOnDriverLoad**会导致框架禁用其他 UMDF 超时（例如即插即用操作）。 这意味着，如果你的驱动程序导致过多的超时，则使用这些值可能导致驱动程序导致目标出现严重故障。

还可以使用 WDK 中包含的 WDF 验证程序工具（您尚未 wdfverifier）来设置这些注册表值。 有关将此工具用于 UMDF 驱动程序的信息，请参阅使用[WDF 验证器管理 UMDF 验证程序设置](https://docs.microsoft.com/windows-hardware/drivers/devtest/global-wdf-settings-tab)。

这些附加值位于**HKLM\\\\SOFTWARE Microsoft\\Windows NT\\CurrentVersion\\WUDF\\DebugMode**：

## <a name="debugmodeflags"></a>DebugModeFlags

*REG\_DWORD，仅 UMDF*

|“值”|说明|
|--- |--- |
|0x01|启用调试模式。 此设置关闭在[UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)中所述的自动重新启动功能。|
|0x02|禁用设备池。 有关设备池的详细信息，请参阅[在 UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。|
|0x04|禁用超时。|
 

在 Microsoft Visual Studio 中使用 F5 选项时，会为部署的驱动程序设置所有三个标志。

## <a name="debugmodebinaries"></a>DebugModeBinaries

*REG\_多\_SZ，仅 UMDF*

此值指定要在调试模式下加载的驱动程序二进制文件的名称。 例如，若要为驱动程序二进制文件 X .DLL、Y .DLL 和 Z .DLL 启用调试模式，此值将设置为*\\w..1 ....。DLL\\0Z\\0\\0*。

还可以在**HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\WUDF**中设置以下值：

## <a name="hostfailkddebugbreak"></a>HostFailKdDebugBreak

*REG\_DWORD，仅 UMDF*

如果此值不为零，并且内核调试器连接到计算机，则在终止宿主进程之前，反射器将进入内核调试器。 默认情况下，在 Windows 7 和更早版本的操作系统中禁用**HostFailKdDebugBreak** 。 从 Windows 8 开始，默认情况下会启用**HostFailKdDebugBreak** 。

如果主机进程意外终止（例如，由于非 UMDF 组件或由于未经处理的异常），则反射器还会中断内核调试器。 如果要终止的主机进程中有多个设备堆栈，则反射器会多次中断到调试器中，一次用于主机进程中加载的每个设备堆栈。

要使对 UMDF 注册表值所做的更改生效，您必须重新启动计算机。
 
