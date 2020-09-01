---
title: Windows 10 中的 WDF 驱动程序新增功能
description: 汇总了 Windows 10 中的 WDF 驱动程序的新功能和改进。
ms.assetid: 61fd9916-38e7-47d0-aec7-d5a489eb21eb
keywords:
- 内核模式驱动程序 WDK KMDF, 关于 KMDF
- KMDF WDK, 关于 KMDF
- 内核模式驱动程序框架 WDK, 关于 KMDF
- 基于框架的驱动程序 WDK KMDF
- 基于框架的驱动程序 WDK KMDF, 关于基于框架的驱动程序
- 对象 WDK KMDF
- 框架对象 WDK KMDF
ms.date: 10/02/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.custom: 19H1
ms.openlocfilehash: da36860d62fb36ca27658f0bc10372b3ad325f82
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185855"
---
# <a name="whats-new-for-wdf-drivers-in-windows10"></a>Windows 10 中的 WDF 驱动程序新增功能

本主题汇总了 Windows 10 中的 Windows 驱动程序框架 (WDF) 驱动程序的新功能和改进。

Windows 10 版本 1903（2019 年 3 月更新，19H1）包括内核模式驱动程序框架 (KMDF) 版本 1.29 和用户模式驱动程序框架 (UMDF) 版本 2.29。

可以使用这些框架版本为以下操作系统生成驱动程序：

-   Windows 10（所有 SKU）
-   Windows Server 版本 1809

有关版本历史记录，请参阅 [KMDF 版本历史记录](kmdf-version-history.md)和 [UMDF 版本历史记录](umdf-version-history.md)。 除非特别说明，否则本页中的 UMDF 参考介绍的是版本 2 的功能，该功能在 UMDF 版本 1 中不提供。

## <a name="new-in-wdf-for-windows-10-version-2004"></a>适用于 Windows 10 版本 2004 的 WDF 中的新增功能

请参阅 [KMDF 版本历史记录](kmdf-version-history.md)和 [UMDF 版本历史记录](umdf-version-history.md)。

## <a name="new-in-wdf-for-windows-10-version-1903"></a>适用于 Windows 10 版本 1903 的 WDF 中的新功能

未添加或更改任何功能。

## <a name="new-in-wdf-for-windows-10-version-1809"></a>适用于 Windows 10 版本 1809 的 WDF 中的新功能

* 添加了新 API [**WdfDriverRetrieveDriverDataDirectoryString**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring)

## <a name="new-in-wdf-for-windows-10-version-1803"></a>适用于 Windows 10 版本 1803 的 WDF 中的新功能

* [针对多个 Windows 版本生成 WDF 驱动程序](building-a-wdf-driver-for-multiple-versions-of-windows.md)。
* [**WdfDeviceRetrieveDeviceDirectoryString**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring)

## <a name="new-in-wdf-for-windows-10-version-1709"></a>适用于 Windows 10 版本 1709 的 WDF 中的新功能

请参阅 [KMDF 版本历史记录](kmdf-version-history.md)和 [UMDF 版本历史记录](umdf-version-history.md)。

## <a name="new-in-wdf-for-windows-10-version-1703"></a>适用于 Windows 10 版本 1703 的 WDF 中的新功能

在 Windows 10 版本 1703 中，WDF 包含以下增强功能：

* 新的 WDF 验证程序设置，用于检测是否过多地创建了对象
 
    某些情况下，框架对象未正确设置父级且在使用后未删除。  有了此功能，就可以指定对象的最大数目，以及超过此阈值时会发生什么情况。
    
    若要开始监视，请在 `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\<driver service>\Parameters\wdf` 项下添加以下注册表值：
    
  1. 添加名为 **ObjectLeakDetectionLimit** 且带阈值的 DWORD 值。 这是最大的对象数，对象类型如 **ObjectsForLeakDetection** 项中所述。
    
  2. 添加名为 **ObjectsForLeakDetection** 的新 REG_MULTI_SZ 值，用于列出要验证的每个类型名称。 例如，可以指定 `WDFDMATRANSACTION WDFDEVICE`。 若要指定所有句柄类型，请使用 `*` 作为字符串。

  3. 若要控制在超过此阈值的情况下是否应导致调试断点或 Bug 检查，请设置 [DbgBreakOnError](using-kmdf-verifier.md) 项。

     默认情况下，如果 ObjectsForLeakDetection 项未指定，则框架会监视 WDFREQUEST、WDFWORKITEM、WDFKEY、WDFSTRING、WDFOBJECT 和 WDFDEVICE。
    
     此限制随安装的设备数伸缩，因此，如果驱动程序创建了 3 个 WDFDEVICE 对象，则 WDF 验证程序限制是 **ObjectLeakDetectionLimit** 中指定的值的 3 倍。
    
     如果指定 WDFREQUEST，则验证程序仅将驱动程序创建的 WDFREQUEST 对象计入。
    
     此功能当前不支持跟踪 WDFMEMORY 对象类型。 

* SleepStudy 工具提供了有关 KMDF 驱动程序的信息

    SleepStudy 软件工具报告 KMDF 驱动程序具有的妨碍系统进入睡眠的电源参考数。  有关详细信息，请参阅 [Modern standby SleepStudy](/windows-hardware/design/device-experiences/modern-standby-sleepstudy)（新式待机 SleepStudy）。

此页其余部分介绍 Windows 10 版本 1507 中增加的功能。

## <a name="wdf-source-code-is-publicly-available"></a>WDF 源代码已公开发布


-   WDF 源代码现在位于 GitHub 上，以开源方式提供。 Windows 10 中提供的 WDF 运行时库是根据此源代码生成的。 如果能够按照驱动程序和 WDF 之间的交互步骤进行操作，则可更有效地调试驱动程序。 从 <https://github.com/Microsoft/Windows-Driver-Frameworks> 下载它。

-   Windows 10 上的 WDF 的专用符号文件现在可以通 Microsoft 符号服务器获取。

-   Windows 驱动程序工具包 (WDK) 10 示例现在也发布到 GitHub。 从 <https://github.com/Microsoft/Windows-Driver-Samples> 下载它们。

## <a name="automatic-source-level-debugging-of-framework-code"></a>自动对框架代码进行源级别调试


使用 WinDbg 调试 Windows 10 上的 WDF 驱动程序时，WinDbg 会自动从 Microsoft 的公共 GitHub 存储库检索框架源代码。 可以通过此功能在调试时单步执行 WDF 源代码，了解框架的内部结构，不需将源代码下载到本地计算机。 有关详细信息，请参阅 [New support for source-level debugging of WDF code in Windows 10](https://go.microsoft.com/fwlink/p/?LinkId=618534)（全新支持：在 Windows 10 中对 WDF 代码进行源级别调试）、[Debugging with WDF Source](https://go.microsoft.com/fwlink/p/?LinkId=618535)（通过 WDF 源进行调试）并观看[视频：使用 WDF 源代码调试驱动程序](video--debugging-your-driver-with-wdf-source-code.md)。

## <a name="universal-driver-compliance"></a>通用驱动程序符合性


所有 WDF 驱动程序示例和 Visual Studio 驱动程序模板都兼容[通用 Windows 驱动程序](/windows-hardware/drivers)。

所有 KMDF 和 UMDF 2 功能都兼容通用 Windows 驱动程序。

请注意，UMDF 1 驱动程序仅在 Windows 10 桌面版和早期的 Windows 桌面版上运行。 想要使用 UMDF 2 的通用功能？ 若要了解如何移植旧的 UMDF 1 驱动程序，请参阅[将驱动程序从 UMDF 1 移植到 UMDF 2](porting-a-driver-from-umdf-1-to-umdf-2.md)。

## <a name="debugging-and-diagnosability"></a>调试和诊断能力


-   所有 KMDF 和 UMDF 2 驱动程序都可以使用一个始终打开且始终提供的即时跟踪记录器 (IFR)。 当驱动程序提供自定义跟踪时，驱动程序 IFR 日志将包含跟踪消息。 请注意，新的驱动程序 IFR 日志独立于 WDF 为每个驱动程序创建的框架 IFR 日志。

    很容易就可以打开 IFR。 请参阅 [Inflight Trace Recorder (IFR) for logging traces](../devtest/using-wpp-recorder.md)（用于记录跟踪的即时跟踪记录器 (IFR)）和[在 KMDF 和 UMDF 驱动程序中使用即时跟踪记录器](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)。

-   IFR 在不可分页的内存中保留一个循环缓冲区，其中有 WPP 跟踪。 如果驱动程序出现故障，则会在故障转储文件中频繁保存日志。

-   如果在驱动程序二进制文件中启用 IFR，则在驱动程序的生命周期内，IFR 会始终存在并处于运行状态。 不需启动显式跟踪收集会话。

    -   IFR 日志包含在小型转储文件中，除非相应的驱动程序未确定或者该崩溃是主机超时。

    -   如果连接了调试程序，则可通过发出 [ **!wdfkd.wdflogdump**](../debugger/-wdfkd-wdflogdump.md) 来访问驱动程序和框架 IFR 日志。

    -   即使未连接调试程序，也可以访问这两种日志。  若要了解具体方法，请观看[视频：在没有调试程序的情况下访问驱动程序 IFR 日志](video--accessing-driver-ifr-logs-without-a-debugger.md)。

    -   调试 UMDF 驱动程序时，可以将框架日志与驱动程序日志合并在一起，方法是发出以下命令：!wdfkd.wdflogdump  &lt;drivername.dll&gt;  -m 

-   UMDF 日志 (WudfTrace.etl) 和转储现在位于 %ProgramData%\\Microsoft\\WDF 中而不是 %systemDrive%\\LogFiles\\Wudf 中。

-   可以通过新的调试程序命令 [ **!wdfkd.wdfumtriage**](../debugger/-wdfkd-wdfumtriage.md) 以内核为中心查看系统中的所有 UMDF 设备。

-   可以运行 [ **!analyze**](../debugger/-analyze.md) 来调查 UMDF 验证程序故障或 UMDF 未处理异常。 这适用于实时内核调试，以及对 *%ProgramData%* \\Microsoft\\WDF 中的用户故障转储文件进行的调试。

-   在 KMDF 和 UMDF 2 中，可以在调试程序中监视电源参考使用情况。 有关信息，请参阅[在 WDF 中调试电源参考漏孔](debugging-power-reference-leaks-in-wdf.md)。

-   可以使用 [ **!wdfkd.wdfcrashdump**](../debugger/-wdfkd-wdfcrashdump.md) 显示有关 UMDF 2 驱动程序的错误信息。 有关详细信息，请参阅 **!wdfkd.wdfcrashdump**。

## <a name="performance-tracing-tool-for-wdf-drivers"></a>用于 WDF 驱动程序的性能跟踪工具


可以使用 Windows 性能工具包 (WPT) 查看给定的 KMDF 或 UMDF 2 驱动程序的性能数据。 启用跟踪时，框架会针对 I/O、PnP 和电源回调路径生成 ETW 事件。 然后，你可以在 Windows Performance Analyzer (WPA) 中查看各种图，了解 I/O 吞吐率、CPU 使用率和回调性能。 WPT 包括在 Windows 评估和部署工具包 (ADK) 中。

有关详细信息，请参阅 [New Performance Tools for WDF Drivers in Windows 10]( https://go.microsoft.com/fwlink/p/?LinkId=618537)（Windows 10 中用于 WDF 驱动程序的全新性能工具）和[将 Windows 性能工具包 (WPT) 与 WDF 配合使用](using-the-windows-performance-toolkit--wpt--with-wdf.md)。

## <a name="additional-support-for-hid-drivers-in-umdf"></a>针对 UMDF 中的 HID 驱动程序的其他支持


-   UMDF 现在完全支持 HID 筛选器（按 HIDClass 枚举）和微型驱动程序。 直接移植现有的 KMDF 驱动程序或编写新的 UMDF 2 筛选器，然后系统就会自动启用该功能。

-   按 ACPI 枚举的 UMDF HID 微型驱动程序可以执行选择性挂起。 有关详细信息，请参阅[创建 WDF HID 微型驱动程序](creating-umdf-hid-minidrivers.md)。

-   UMDF 驱动程序现在可以安装在 HID 堆栈中，用于低延迟输入设备，例如触控和鼠标。 用于输入设备的驱动程序应该指定 **UmdfHostPriority** INF 指令。 有关信息，请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。

## <a name="support-for-interrupts-for-gpio-backed-devices"></a>支持的中断适用于 GPIO 支持的设备


-   UMDF 2 支持的中断适用于 GPIO 支持的设备，例如硬件推送按钮。 KMDF 为这些设备提供本机支持，不需使用[处理同时处于活动状态的中断](handling-active-both-interrupts.md)中所述的解决方法。 有关详细信息，请参阅[创建中断对象](creating-an-interrupt-object.md)。

## <a name="umdf-no-longer-requires-winusb"></a>UMDF 不再需要 WinUSB


为 UMDF 中的 USB 驱动程序添加了新的支持。 UMDF 2 USB 驱动程序不再使用 WinUSB。 为了使用新的功能，驱动程序将 **UmdfDispatcher** 指令设置为 **NativeUSB** 而不是 **WinUSB**。 请参阅[在 INF 文件中指定 WDF 指令](specifying-wdf-directives-in-inf-files.md)。


## <a name="improved-performance"></a>改进的性能


-   UMDF 系统组件占用较少的磁盘空间。

-   KMDF 和 UMDF 驱动程序使用较少的非分页内存。

-   改进的框架版本检查功能减少了标头/库不匹配项。

-   UMDF 为 HID 传输提供改进的缓冲区映射。

 

