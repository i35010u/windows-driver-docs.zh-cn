---
title: 使用框架的事件记录器
description: 使用框架的事件记录器
ms.assetid: aa0a83c8-cd13-41d0-a619-d8793b2e2e80
keywords:
- 调试驱动程序 WDK KMDF，事件记录器
- 事件记录器 WDK KMDF
- 正在进行的录制器 WDK KMDF
- IFR WDK KMDF
- WDK KMDF，日志记录的事件
- 错误 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf514b5569526f8b125b236b6979d0ccb949b177
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562074"
---
# <a name="using-the-frameworks-event-logger"></a>使用框架的事件记录器


WDF 包括有时称为框架的内部跟踪记录器*正在进行录制器*(IFR)。 WDF 记录器创建包含事件的每个 WDF 驱动程序的最新历史记录的跟踪日志。 跟踪日志跟踪通过框架和驱动程序通过将相应请求的 I/O 请求数据包 (Irp) 的进度。 每个内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序具有其自己的日志。

WDF 记录器始终处于启用状态。 为每个跟踪日志，记录器将事件记录存储在循环的内存缓冲区中。 或者，您可以打开详细级别，它会导致其他信息可帮助你调试您的驱动程序，如条目记录到事件记录器或退出从内部的代码路径。 默认情况下，缓冲区的大小是一个内存页和详细程度处于关闭状态。 可以通过调整这些值在中的更改缓冲区的大小和详细程度[WdfVerifier 应用程序](https://msdn.microsoft.com/library/windows/hardware/ff556129)。 请注意，开启详细级别可能会降低系统性能。

WDF 调试器扩展可用于查看和交互调试期间保存 WDF 日志。 若要在调试会话期间查看 WDF 日志：

1.  加载正确的符号。 可以使用[ **.symfix**](https://msdn.microsoft.com/library/windows/hardware/ff565400)+ 调试器命令，以将 Microsoft 公共符号存储区追加到现有的符号路径。 公共符号存储区包括 WDF 二进制文件的符号。 您可能想要加载的驱动程序符号的符号。

    有关如何获取其他信息窗口符号和如何设置调试器的符号路径，请参阅随提供的文档[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)包。

2.  负载[Wdfkd.dll 扩展插件库](debugger-extensions-for-kmdf-drivers.md)在调试器中。 如果使用的内核调试程序，可以执行此操作通过使用[ **.load** ](https://msdn.microsoft.com/library/windows/hardware/ff563964)命令。 若要加载正确版本的 Wdfkd.dll 需要指定 DLL 的完全限定的路径。 例如，将基于 x86 的调试器主机计算机上使用以下路径：

    ```cpp
    .load "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\wdfkd.dll"
    ```

    然后可以确认使用加载该扩展[ **！ 链**](https://msdn.microsoft.com/library/windows/hardware/ff562212)命令以显示所有已加载的扩展。

    有关框架调试器扩展的详细信息，请使用[ **！ wdfhelp** ](https://msdn.microsoft.com/library/windows/hardware/ff565761)扩展。 有关内核调试程序的详细信息，请参阅随提供的文档[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)包。

3.  如果您的驱动程序使用框架版本 1.11 或更高版本，并使用内核调试程序从 Windows 8 或更高版本，则可以跳过此步骤。

    如果您的驱动程序使用早于 1.11 的 framework 版本，使用[ **！ wdftmffile** ](https://msdn.microsoft.com/library/windows/hardware/ff566128)或[ **！ wdfsearchpath** ](https://msdn.microsoft.com/library/windows/hardware/ff566120)指定特定于平台的跟踪消息格式 (.tmf) 文件或.tmf 文件的路径。 .Tmf 文件位于在 WDK 中的特定于平台的子目录中。

    因为.tmf 文件是特定于版本，必须指定当前正在运行的框架的运行时库的版本相对应的.tmf 文件。 例如，如果主机计算机上运行 KMDF 1.9 版：

    ```cpp
    !wdftmffile c:\WinDDK\<version>\tools\tracing\x86\wdf01009.tmf
    ```

    此外可以通过设置跟踪设置的搜索路径\_格式\_搜索\_PATH 环境变量。 [ **！ Wdftmffile** ](https://msdn.microsoft.com/library/windows/hardware/ff566128)命令优先于由环境变量设置的搜索路径。

    若要验证的 framework 的版本编号，可以运行[ **！ wdfldr** ](https://msdn.microsoft.com/library/windows/hardware/ff565803)调试器从内核调试程序扩展命令。

4.  使用[ **！ wdflogdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565805)扩展以显示事件记录器的记录。 例如，下面的屏幕截图的 WinDbg 命令窗口显示的输出的典型示例 **！ wdflogdump**:

    ![示例的输出 ！ wdflogdump 扩展](images/kmdf-using-wdflogdump.png)

框架的日志中的每一行的前面有一个字符串，调用[跟踪消息前缀](https://msdn.microsoft.com/library/windows/hardware/ff553941)。 跟踪记录器前面添加到每条消息写入到日志的此前缀。 默认情况下，前缀包含一组标准的数据元素，但可以更改默认元素，以满足特定的要求。 您可以通过设置跟踪更改 WDF 驱动程序的前缀字符串\_格式\_前缀环境变量或通过使用[ **！ wdfsettraceprefix** ](https://msdn.microsoft.com/library/windows/hardware/ff566123)调试器扩展命令。

若要设置环境变量，请使用类似于以下的命令：

```cpp
Set TRACE_FORMAT_PREFIX=%2!s!: %!FUNC!: %8!04x!.%3!04x!: %4!s!:
```

此命令将跟踪消息前缀设置为以下：

```cpp
SourceFile_LineNumber: FunctionName: ProcessID.ThreadID: SystemTime
```

此外可以使用[ **！ wdflogsave** ](https://msdn.microsoft.com/library/windows/hardware/ff566102)扩展命令，可以通过查看事件跟踪日志 (.etl) 文件中保存的事件记录器的记录[TraceView](https://msdn.microsoft.com/library/windows/hardware/ff553872)。

有时，您可以使用[ **！ wdfcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565682)调试器上的故障转储后检查系统 bug 显示日志信息的扩展。 日志信息才可用在崩溃转储框架可以确定您的驱动程序导致的 bug 检查，或者如果已设置[ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md)驱动程序的注册表值。

如果调试器已附加 bug 检查发生时，您可以使用[ **！ wdfcrashdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565682)查看日志信息立即，也可以通过查看信息加载内存转储文件。 由于很小的内存转储文件的大小限制，导致发生故障的驱动程序日志可能不会显示在转储。

该框架可以确定特定驱动程序是否导致以下 bug 检查代码：

-   [**Bug 检查 0xD1:DRIVER\_IRQL\_NOT\_LESS\_OR\_EQUAL**](https://msdn.microsoft.com/library/windows/hardware/ff560244)
-   [**Bug 检查 0xA:IRQL\_NOT\_LESS\_OR\_EQUAL**](https://msdn.microsoft.com/library/windows/hardware/ff560129)
-   [**Bug 检查 0x20:KERNEL\_APC\_PENDING\_DURING\_EXIT**](https://msdn.microsoft.com/library/windows/hardware/ff557421)
-   [**Bug 检查 0x8e 越权：内核\_模式下\_异常\_不\_已处理**](https://msdn.microsoft.com/library/windows/hardware/ff559271)
-   [**Bug 检查 0x1E:KMODE\_异常\_不\_已处理**](https://msdn.microsoft.com/library/windows/hardware/ff557408)
-   [**Bug 检查 0x50:页\_容错\_IN\_未分页\_区域**](https://msdn.microsoft.com/library/windows/hardware/ff559023)
-   [**Bug 检查 0x7E:系统\_线程\_异常\_不\_已处理**](https://msdn.microsoft.com/library/windows/hardware/ff559239)

从 UMDF 版本 2 开始，UMDF 存储 UMDF 跟踪日志 (或 UMDF *IFR*) 内核非分页内存中。 该框架会分配一个 IFR 每个驱动程序主机 (Wudfhost) 实例。

有关调试器扩展命令的详细信息，请参阅[基于框架的驱动程序的调试器扩展](debugger-extensions-for-kmdf-drivers.md)。

 

 





