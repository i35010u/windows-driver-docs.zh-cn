---
title: 视频调试带 WDF 源代码的驱动程序
description: 本主题包含视频教程，该教程演示如何调试 Windows 驱动程序框架（WDF）驱动程序对 WDF 源代码具有完全访问权限。
Search.SourceType: Video
ms.assetid: 735D71FC-0B35-4C79-8C0A-F3C762095C06
ms.date: 05/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6cd9703ca9adebf2a77f8bc6c9c5ec020db70180
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141190"
---
# <a name="video-debugging-your-driver-with-wdf-source-code"></a>视频：使用 WDF 源代码调试驱动程序


本主题包含视频教程，该教程演示如何调试 Windows 驱动程序框架（WDF）驱动程序对 WDF 源代码具有完全访问权限。 视频后面是视频后面的分步过程，用于方便引用。


>[!VIDEO https://www.microsoft.com/videoplayer/embed/2568bc8a-3f0b-4900-b659-aa5b22159f04]

WDF 源调试允许无需下载 WDF 源代码即可随意单步执行框架代码。 调试器会自动从 GitHub 下载正确的 WDF 版本。

例如，如果你使用 WinDbg 在 Windows 10 计算机上调试 WDF 驱动程序，并且使用调用堆栈中的框架代码使调试器中断，则可以在 "调用堆栈" 视图中双击 WDF 帧，然后将自动下载并在匹配行中打开相关的 WDF 源文件。 然后，可以单步执行代码并设置断点。

此功能适用于运行 Windows 10 公共版本、Technical Preview 版本10041或更高版本的目标系统。 这些生成具有 Microsoft 公共符号服务器上提供的 KMDF （Wdf01000.sys）和 UMDF （Wudfx02000.dll）的专用源索引符号文件。 WDF 代码的源级别调试仅适用于 WinDbg，不适用于 Visual Studio 调试器。

## <a name="quick-start"></a>快速启动

在目标计算机上启动 WinDbg 内核调试会话，中断，然后执行以下步骤：

1. 使用 symfix 设置默认符号路径。 这会将符号路径设置为指向处的符号服务器 https://msdl.microsoft.com/download/symbols 。

    `kd> .symfix`

2. 使用 srcfix 设置默认源路径。 这会将源路径设置为 srv *，这会告诉调试器从目标模块的符号文件中指定的位置检索源文件。

    ```
    kd> .srcfix
    Source search path is: SRV*
    ```

3. 使用重新加载符号，并确认 Wdf01000.sys 的符号（或 UMDF 的 Wudfx02000.dll）已进行源索引。 如下面的 lmi 的输出中所示，Wdf01000.sys PDB 为源索引。 如果不是，请参阅下面的 WinDbg 设置部分。

    ```
    kd> .reload
    ...

    kd> !lmi wdf01000.sys
    Loaded Module Info: [wdf01000.sys] 
    ...
    Load Report: private symbols & lines, source indexed 
    C:\...\Wdf01000.pdb\...\Wdf01000.pdb
    ```

4. 现在已经完成了！ 单步执行 WDF 源代码的简单方法是在框架的 IRP 调度例程上设置一个断点，然后单步执行代码的其余部分。 由于 Windows 系统具有多个收件箱 KMDF 驱动程序，因此，WDF 始终会加载并运行，因此，将立即点击此断点（无需加载自己的驱动程序）。

    ```
    kd> bp Wdf01000!FxDevice::DispatchWithLock
    kd> g
    Breakpoint 0 hit
    Wdf01000!FxDevice::DispatchWithLock:
    87131670 8bff mov edi,edi 
    ```

如果这不起作用，请查看以下 WinDbg 设置步骤。 

## <a name="windbg-setup"></a>WinDbg 设置

如果上面的示例未按预期工作，则可能需要执行以下一个或多个说明。

### <a name="enable-source-mode-debugging"></a>启用源模式调试

请确保已启用[源模式下的调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-in-source-mode)。 打开 "调试" 菜单，确认已选中 "源" 模式。


 
### <a name="clear-stale-symbols-cache"></a>清除过时符号缓存

如果以前为同一个 Windows 目标调试了 WDF 驱动程序，则可能使用本地缓存的不是源索引的 WDF 符号。 可以通过！ lmi 命令进行检查：

```cmd
kd> !lmi Wdf01000.sys
Loaded Module Info: [wdf01000.sys]
...
Load Report: private symbols & lines, not source indexed
C:\...\Wdf01000.pdb\...\Wdf01000.pdb
```

根据上面的负载报告，Wdf01000 未索引源。 这意味着本地 WinDbg 符号缓存已过时。 若要解决此问题，请从 WinDbg 中卸载 PDB，清除本地缓存（根据上面的！ lmi 输出，路径可能有所不同），并重新加载 PDB：

```cmd
kd> .reload /u Wdf01000.sys

CMD> del
C:\...\Wdf01000.pdb\...\Wdf01000.pdb

kd> .reload Wdf01000.sys
```

现在，运行！ lmi 再次检查： PDB 应显示为 "源索引"，并且应弹出源代码窗口。

```cmd
kd> !lmi Wdf01000.sys
Loaded Module Info: [wdf01000.sys]
...
Load Report: private symbols & lines, source indexed
C:\...\Wdf01000.pdb\...\Wdf01000.pdb 
```

您可以使用 WDF 源级调试来实现实时调试和分析故障转储，还可以通过设置核心函数（如 IRP 调度程序和浏览后续代码路径）上的断点来了解有关框架内部的详细信息。



