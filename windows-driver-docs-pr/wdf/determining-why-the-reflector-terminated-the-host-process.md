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
ms.openlocfilehash: 0820f51e5e878c27ebadb7875248fa83f918c21d
ms.sourcegitcommit: 9355a80229bb2384dd45493d36bdc783abdd8d7a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694243"
---
# <a name="determining-why-the-reflector-terminated-the-host-process"></a>确定反射器终止主机进程的原因


本主题介绍如何分析反射器终止驱动程序主机进程（WUDFHost）的原因。

反射器终止宿主进程的最常见原因是： UMDF[主机进程超时](how-umdf-enforces-time-outs.md)。

我们强烈建议使用连接到测试系统的内核调试器并在 WUDFHost 上启用[应用程序验证工具（AppVerif）](../debugger/debugger-download-tools.md) ，来完成 UMDF 驱动程序的开发和测试。 使用以下命令，附加内核调试器，然后重新启动。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

## <a name="using-dump-files"></a>使用转储文件


对于许多崩溃，转储文件详细信息足以确定发生终止的原因。 若要查看转储文件信息，请执行以下步骤：

1.  在% windir%\\system32 中找到最新的 dmp 文件，\\日志文件\\WUDF 目录。

    **请注意**  在 UMDF 2.15 开始，日志目录为 *% ProgramData%* \\Microsoft\\WDF。

     

2.  使用以下命令将最新的 dmp 文件加载到调试器中：
    ```cpp
    WinDbg -z <path to the .dmp file>
    ```

3.  查看终止时线程的状态。

## <a name="using-the-debugger"></a>使用调试器


在其他情况下，可能需要附加到实时内核模式目标来确定反射器终止宿主进程的原因。 若要设置调试会话，请按照[如何启用 UMDF 驱动程序调试](enabling-a-debugger.md#kd)中所述的步骤进行操作。

建立连接后，请使用！ wdfkd 来检查 UMDF 驱动程序，使用[ **！ wdfkd. wdfumirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps) umdf 调试程序扩展显示未完成的[**irp （wdfumtriage**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umirps)版本1）。

-   如果 PnP IRP 或 power IRP 处于挂起状态，请通过检查主机进程中的线程来确定驱动程序导致 IRP 挂起的原因。

    您可以使用[ **！进程**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process)扩展来检查在宿主进程中运行的线程。 **0x1f** flags 值显示每个线程的堆栈跟踪。

    **！进程** *&lt;进程地址&gt;* **0x1f**

-   如果你的驱动程序未快速完成已取消的 IRP，请确定取消了哪个 IRP 以及它未完成的原因。
-   如果清理或关闭 IRP 处于挂起状态，则确定 IRP 需要很长时间才能处理。

 

 





