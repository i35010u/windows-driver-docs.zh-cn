---
title: 确定反射器终止主机进程的原因
description: 本主题介绍如何分析反射器终止驱动程序主机进程（WUDFHost）的原因。
ms.assetid: c80b117b-597a-494a-bc28-5a918d2a9279
keywords:
- 调试方案 WDK UMDF，反射器终止宿主进程
- UMDF WDK，调试方案，反射器终止宿主进程
- UMDF WDK，反射器终止宿主进程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33c5b269e780b4b25993fea88a26800390e230e4
ms.sourcegitcommit: 7dff2005387294dbfeeec45c801bf6b4a4cb9319
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2020
ms.locfileid: "80261287"
---
# <a name="determining-why-the-reflector-terminated-the-host-process"></a>确定反射器终止主机进程的原因


本主题介绍如何分析反射器为什么终止了驱动程序主机进程（WUDFHost）或驱动程序主机进程崩溃的原因。

反射器终止宿主进程的最常见原因是： UMDF[主机进程超时](how-umdf-enforces-time-outs.md)。

我们强烈建议使用连接到测试系统的内核调试器并在 WUDFHost 上启用[应用程序验证工具（AppVerif）](../debugger/debugger-download-tools.md) ，来完成 UMDF 驱动程序的开发和测试。 使用以下命令，附加内核调试器，然后重新启动。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

## <a name="using-dump-files"></a>使用转储文件


如果 UMDF 驱动程序崩溃或遇到问题，则会在内核调试器中报告中断。 当在内核调试器中报告用户模式异常时，应调试这些问题。 内核调试器中断还会通过 WudfRd 在终止驱动程序主机进程之前进行报告，因为该驱动程序有问题（无响应）。 你还会发现在以下位置报告的日志和堆转储。 若要查看 UMDF 捕获的转储文件，请遵循以下步骤：

1.  找到 *% ProgramData%* \\MICROSOFT\\WDF 目录中的最新 dmp 文件。
    在 Windows 10 1507 随附的 UMDF 2.15 之前，日志目录低于% windir%\\system32\\日志记录\\WUDF。

2.  使用以下命令将最新的 dmp 文件加载到调试器中：
    ```cpp
    WinDbg -z <path to the .dmp file>
    ```

3.  查看终止时线程的状态。

如果需要捕获堆转储，则在测试时，在运行测试之前设置以下注册表值并重新启动测试系统。 你还可以在%SystemRoot%\System32\Winevt\Logs\Application.evtx 上检查系统的应用程序事件日志中的 Windows 错误报告历史记录。 

```cpp
reg add "HKLM\Software\Microsoft\windows NT\CurrentVersion\Wudf" /v LogMinidumpType /t REG_DWORD /d 0x1122
reg add "HKLM\Software\Microsoft\windows NT\CurrentVersion\Wudf" /v LogEnable /t REG_DWORD /d 1 
```

## <a name="using-the-debugger"></a>使用调试器

在其他情况下，可能需要附加到实时内核模式目标来确定反射器终止宿主进程的原因。 若要设置调试会话，请按照[如何启用 UMDF 驱动程序调试](enabling-a-debugger.md#kd)中所述的步骤进行操作。

建立连接后，请使用！ wdfkd 来检查 UMDF 驱动程序，使用[ **！ wdfkd. wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps) umdf 调试程序扩展显示未完成的[**irp （wdfumtriage**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umirps)版本1）。

-   如果 PnP IRP 或 power IRP 处于挂起状态，请通过检查主机进程中的线程来确定驱动程序导致 IRP 挂起的原因。

    您可以使用[ **！进程**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process)扩展来检查在宿主进程中运行的线程。 **0x1f** flags 值显示每个线程的堆栈跟踪。

    **！进程** *&lt;进程地址&gt;* **0x1f**

-   如果你的驱动程序未快速完成已取消的 IRP，请确定取消了哪个 IRP 以及它未完成的原因。
-   如果清理或关闭 IRP 处于挂起状态，则确定 IRP 需要很长时间才能处理。

 

 
