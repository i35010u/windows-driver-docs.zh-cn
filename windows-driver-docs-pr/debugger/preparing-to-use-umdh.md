---
title: 准备使用 UMDH
description: 准备使用 UMDH
keywords:
- UMDH，准备使用 UMDH
- UMDH，禁用 BSTR 缓存
- SetNoOaCache 函数
- OANOCACHE 环境变量
- 堆栈跟踪数据库
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 728983e4bd6f633f562428bb9feacc9384ce9228
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793235"
---
# <a name="preparing-to-use-umdh"></a>准备使用 UMDH

必须先完成本部分所述的配置任务，然后才能使用 User-Mode 转储堆 (UMDH) 捕获进程的堆分配。 如果计算机配置不正确，UMDH 将不会生成任何结果，也不会导致结果不完整或不正确。

### <a name="create-the-user-mode-stack-trace-database"></a>创建用户模式堆栈跟踪数据库

使用 UMDH 捕获进程的堆分配之前，必须将 Windows 配置为捕获堆栈跟踪。

若要为进程启用堆栈跟踪捕获，请使用 [GFlags](gflags.md) 为进程设置 " **创建用户模式堆栈跟踪数据库** " 标志。 可以通过以下任一方法完成此操作：

-   在 GFlags 图形界面中，选择 " **图像文件** " 选项卡。键入进程名称，包括文件扩展名 (例如 Notepad.exe) 。 按 **tab** 键，选择 " **创建用户模式堆栈跟踪数据库**"，然后选择 " **应用**"。

-   或者，使用以下 GFlags 命令行，其中 *ImageName* 是进程名称 (包括文件扩展名) ：

    **gflags/I** *ImageName* **+ ust**

默认情况下，在 x86 处理器上 Windows 收集的堆栈跟踪数据量限制为 32 MB，在 x64 处理器上限制为 64 MB。 如果必须增加此数据库的大小，请选择 "GFlags" 图形界面中的 " **映像文件** " 选项卡，键入进程名称，按 **tab** 键，选中 " **Stack Backtrace (Megs)** " 复选框，在 "关联" 文本框中键入值 (，以) MB 为单位），然后选择 " **应用**"。

**注意**   仅在必要时增加此数据库，因为它可能会耗尽有限的 Windows 资源。 如果不再需要更大的大小，则将此设置返回到其原始值。

这些设置会影响程序的所有新实例。 它不会影响当前正在运行的程序实例。

### <a name="access-the-necessary-symbols"></a>访问必需的符号

使用 UMDH 之前，必须有权访问应用程序的正确符号。 UMDH 使用环境变量 \_ NT 符号路径指定的符号路径 \_ \_ 。 将此变量设置为包含应用程序的符号的路径。

如果还包括 Windows 符号的路径，则分析可能更完整。 此符号路径的语法与调试器使用的语法相同;有关详细信息，请参阅 [符号路径](symbol-path.md)。

例如，如果应用程序的符号位于 C： \\ MyApp \\ 符号上，并且已将 Windows 符号文件安装到 \\ \\ myshare \\ winsymbols，则可以使用以下命令设置符号路径：

```console
set _NT_SYMBOL_PATH=c:\myapp\symbols;\\myshare\winsymbols
```

作为另一个示例，如果你的应用程序的符号位于 C： \\ MyApp \\ 符号上，并且你想要为你的 Windows 符号使用公共 Microsoft 符号存储区，则使用 C： \\ MyCache 作为下游存储，你将使用以下命令设置你的符号路径：

```console
set _NT_SYMBOL_PATH=c:\myapp\symbols;srv*c:\mycache*https://msdl.microsoft.com/download/symbols
```

**重要提示**  假设您有两台计算机：一 *台日志记录计算机* ，您可以在其中创建 UMDH 日志以及分析 UMDH 日志的 *分析计算机* 。 分析计算机上的符号路径必须指向在日志记录时日志记录计算机上加载的 Windows 版本的符号。 不要将分析计算机上的符号路径指向符号服务器。 如果这样做，UMDH 将检索分析计算机上运行的 Windows 版本的符号，UMDH 将不会显示有意义的结果。


### <a name="disable-bstr-caching"></a>禁用 BSTR 缓存

自动化 (以前称为 OLE 自动化) 缓存由 BSTR 字符串使用的内存。 这可以防止 UMDH 正确确定内存分配的所有者。 若要避免此问题，必须禁用 BSTR 缓存。

若要禁用 BSTR 缓存，请将 OANOCACHE 环境变量设置为等于 1)  (。 必须在启动要跟踪其分配的应用程序之前进行此设置。

或者，通过调用 .NET Framework **SetNoOaCache** 函数，可以在应用程序本身中禁用 BSTR 缓存。 如果选择此方法，应提前调用此函数，因为调用 **SetNoOaCache** 时已缓存的任何 BSTR 分配都将保持缓存。

如果需要跟踪服务所做的分配，则必须将 OANOCACHE 设置为系统环境变量，然后重新启动 Windows，使此设置生效。

### <a name="find-the-process-id"></a>查找进程 ID

UMDH 通过进程标识符 (PID) 来标识进程。 您可以使用任务管理器、Tasklist 或 [tlist.exe](tlist.md)查找任何正在运行的进程的 PID。

 

 





