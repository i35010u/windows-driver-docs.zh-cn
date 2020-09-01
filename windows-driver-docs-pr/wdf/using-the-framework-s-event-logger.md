---
title: 使用框架的事件记录器
description: 使用框架的事件记录器
ms.assetid: aa0a83c8-cd13-41d0-a619-d8793b2e2e80
keywords:
- 调试驱动程序 WDK KMDF，事件记录器
- 事件记录器 WDK KMDF
- 正在进行的录音机 WDK KMDF
- IFR WDK KMDF
- 事件 WDK KMDF，日志记录
- 错误 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbe7ba5400812e9c2744fc361605ddfcc72bff42
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191219"
---
# <a name="using-the-frameworks-event-logger"></a>使用框架的事件记录器


WDF 包含内部跟踪记录器，有时称为框架的 *正在进行的记录器* (IFR) 。 WDF 记录器会创建一个跟踪日志，其中包含每个 WDF 驱动程序的最新事件历史记录。 跟踪日志跟踪 i/o 请求包的进度 (Irp) 通过通过驱动程序的框架和相应的请求。 每个内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序都有自己的日志。

WDF 记录器始终处于启用状态。 对于每个跟踪日志，记录器将事件记录存储在循环内存缓冲区中。 或者，您可以打开详细级别，这会使事件记录器记录可帮助您调试驱动程序的其他信息，例如，输入到内部代码路径或从内部代码路径中退出。 默认情况下，缓冲区的大小为一个内存页，详细级别为关闭。 通过在 [您尚未 wdfverifier 应用程序](../devtest/wdf-verifier-control-application.md)中调整这些值，可以更改缓冲区的大小和详细级别。 请注意，启用详细级别可能会降低系统性能。

您可以使用 WDF 调试器扩展在交互式调试过程中查看并保存 WDF 日志。 在调试会话期间查看 WDF 日志：

1.  加载正确的符号。 可以使用 [**. symfix**](../debugger/-symfix--set-symbol-store-path-.md)+ 调试器命令将 Microsoft 公共符号存储区追加到现有的符号路径。 公共符号存储区包含 WDF 二进制文件的符号。 你可能还希望为驱动程序符号加载符号。

    有关如何获取窗口符号以及如何设置调试器符号路径的其他信息，请参阅 [Windows 调试](../debugger/index.md) 包附带的文档。

2.  将 [Wdfkd.dll 扩展库](debugger-extensions-for-kmdf-drivers.md) 加载到调试器中。 如果你使用的是内核调试器，则可以通过使用 [**load**](../debugger/-load---loadby--load-extension-dll-.md) 命令来执行此操作。 若要加载正确的 Wdfkd.dll 版本，需要指定 DLL 的完全限定路径。 例如，你将在基于 x86 的调试器主机上使用以下路径：

    ```cpp
    .load "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\wdfkd.dll"
    ```

    然后，你可以通过使用 [**！链式**](../debugger/-chain--list-debugger-extensions-.md) 命令显示加载的所有扩展，以确认是否已加载该扩展。

    有关框架调试器扩展的详细信息，请使用 [**！ wdfhelp**](../debugger/-wdfkd-wdfhelp.md) 扩展。 有关内核调试器的详细信息，请参阅 [Windows 调试](../debugger/index.md) 包附带的文档。

3.  如果你的驱动程序使用 framework 1.11 或更高版本，并且你在使用 Windows 8 或更高版本的内核调试器，则可以跳过此步骤。

    如果驱动程序使用的框架版本早于1.11，请使用 [**！ wdftmffile**](../debugger/-wdfkd-wdftmffile.md) 或 [**！ wdfsearchpath**](../debugger/-wdfkd-wdfsearchpath.md) 指定特定于平台的跟踪消息格式 (. tmf) 文件或 tmf 文件的路径。 Tmf 文件位于 WDK 中特定于平台的子目录中。

    因为 tmf 文件是特定于版本的文件，所以必须指定一个 tmf 文件，该文件对应于当前正在运行的 framework 运行时库版本。 例如，如果 KMDF 版本1.9 正在主机上运行：

    ```cpp
    !wdftmffile c:\WinDDK\<version>\tools\tracing\x86\wdf01009.tmf
    ```

    还可以通过设置跟踪 \_ 格式 \_ 搜索 \_ 路径环境变量来设置搜索路径。 [**！ Wdftmffile**](../debugger/-wdfkd-wdftmffile.md)命令优先于环境变量设置的搜索路径。

    若要验证 framework 版本号，可从内核调试器运行 [**！ wdfldr**](../debugger/-wdfkd-wdfldr.md) 调试器扩展命令。

4.  使用 [**！ wdflogdump**](../debugger/-wdfkd-wdflogdump.md) 扩展显示事件记录器的记录。 例如，WinDbg 命令窗口的以下屏幕截图显示了 **！ wdflogdump**的输出的典型示例：

    ![！ wdflogdump 扩展中的示例输出](images/kmdf-using-wdflogdump.png)

框架日志中的每一行前面都有一个名为 [跟踪消息前缀](../devtest/trace-message-prefix.md)的字符串。 跟踪记录器将此前缀预置到写入到日志中的每个消息。 默认情况下，前缀包含一组标准数据元素，但您可以更改默认元素以满足您的特定要求。 可以通过设置跟踪 \_ 格式 \_ 前缀环境变量或使用 [**！ wdfsettraceprefix**](../debugger/-wdfkd-wdfsettraceprefix.md) 调试器扩展命令，来更改 WDF 驱动程序的前缀字符串。

若要设置环境变量，请使用与下面类似的命令：

```cpp
Set TRACE_FORMAT_PREFIX=%2!s!: %!FUNC!: %8!04x!.%3!04x!: %4!s!:
```

此命令将跟踪消息前缀设置为以下内容：

```cpp
SourceFile_LineNumber: FunctionName: ProcessID.ThreadID: SystemTime
```

你还可以使用 [**！ wdflogsave**](../debugger/-wdfkd-wdflogsave.md) extension 命令将事件记录器的记录保存到可使用 [TraceView](../devtest/traceview.md)查看的事件跟踪日志 ( .etl) 文件中。

有时可以在崩溃转储中使用 [**！ wdfcrashdump**](../debugger/-wdfkd-wdfcrashdump.md) 调试器扩展，以便在系统 bug 检查后显示日志信息。 仅当框架可以确定驱动程序导致错误检查或为驱动程序设置 [ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md) 注册表值时，才会在故障转储中提供日志信息。

如果在发生 bug 检查时附加了调试器，则可以使用 [**！ wdfcrashdump**](../debugger/-wdfkd-wdfcrashdump.md) 立即查看日志信息，也可以通过加载内存转储文件来查看信息。 由于小内存转储文件的大小限制，导致崩溃的驱动程序的日志可能不会出现在转储中。

框架可以确定特定驱动程序是否导致了以下 bug 检查代码：

-   [**Bug 检查0xD1：驱动程序 \_ IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xd1--driver-irql-not-less-or-equal.md)
-   [**Bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xa--irql-not-less-or-equal.md)
-   [**Bug 检查0x20： \_ \_ \_ 退出期间内核 APC \_ 挂起**](../debugger/bug-check-0x20--kernel-apc-pending-during-exit.md)
-   [**Bug 检查0x8E： \_ \_ \_ 未处理内核模式 \_ 异常**](../debugger/bug-check-0x8e--kernel-mode-exception-not-handled.md)
-   [**Bug 检查0x1E： \_ \_ 未处理 KMODE \_ 异常**](../debugger/bug-check-0x1e--kmode-exception-not-handled.md)
-   [**Bug 检查0x50： \_ \_ \_ 非分页区域中的页错误 \_**](../debugger/bug-check-0x50--page-fault-in-nonpaged-area.md)
-   [**Bug 检查0x7E：系统 \_ 线程 \_ 异常 \_ 未 \_ 处理**](../debugger/bug-check-0x7e--system-thread-exception-not-handled.md)

从 UMDF 版本2开始，UMDF 在内核非分页内存中存储 UMDF 跟踪日志 (或 UMDF *IFR*) 。 框架将每个驱动程序主机 (Wudfhost) 实例分配一个 IFR。

有关调试器扩展命令的详细信息，请参阅 [基于框架的驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

 

