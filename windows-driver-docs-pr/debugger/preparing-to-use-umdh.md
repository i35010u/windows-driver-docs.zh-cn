---
title: 准备使用 UMDH
description: 准备使用 UMDH
ms.assetid: 9adebe43-3167-4e1a-ac98-db19ace944be
keywords:
- UMDH，准备使用 UMDH
- UMDH，禁用 BSTR 缓存
- SetNoOaCache 函数
- OANOCACHE 环境变量
- 堆栈跟踪数据库
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6614f26f908dea52edbf0b1d8a71bf0ae618135
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547828"
---
# <a name="preparing-to-use-umdh"></a>准备使用 UMDH


## <span id="ddk_preparing_to_use_umdh_dtools"></span><span id="DDK_PREPARING_TO_USE_UMDH_DTOOLS"></span>


必须完成使用用户模式转储堆 (UMDH) 捕获进程堆分配之前在本部分中所述的配置任务。 如果计算机未正确配置，UMDH 将不会生成任何结果，或结果将不完整或不正确。

### <a name="span-idcreatetheusermodestacktracedatabasespanspan-idcreatetheusermodestacktracedatabasespancreate-the-user-mode-stack-trace-database"></a><span id="create_the_user_mode_stack_trace_database"></span><span id="CREATE_THE_USER_MODE_STACK_TRACE_DATABASE"></span>创建用户模式堆栈跟踪数据库

使用之前 UMDH 捕获进程堆分配，必须配置 Windows 以捕获的堆栈跟踪。

若要启用堆栈跟踪捕获的进程，请使用[GFlags](gflags.md)若要设置**创建用户模式堆栈跟踪数据库**进程的标志。 这可以通过以下方法之一：

-   在 GFlags 图形界面中，选择**映像文件**选项卡。键入进程名称，其中包括文件扩展名 (例如，Notepad.exe)。 按**选项卡**密钥，请选择**创建用户模式堆栈跟踪数据库**，然后单击**应用**。

-   或者，也可以说，使用以下 GFlags 命令行，其中*ImageName*进程名称 （包括文件扩展名）：

    **gflags /i** *ImageName* **+ust**

默认情况下，Windows 将收集的堆栈跟踪数据量是限制为 32 MB x86 处理器和 64 MB 在 x64 处理器。 如果必须增加此数据库的大小，请选择**映像文件**GFlags 图形界面中的选项卡上，键入进程名称，按**选项卡**项，检查**堆栈回溯 （兆字节）** 复选框，在关联的文本框中，键入一个值 （以 mb 为单位），然后单击**应用**。

**请注意**  增加时有必要，则只有此数据库，因为它可能会耗尽有限的 Windows 资源。 当不再需要较大的大小时，则将此设置恢复到其原始值。

 

这些设置会影响程序的所有新实例。 它不会影响当前正在运行的程序实例。

### <a name="span-idaccessthenecessarysymbolsspanspan-idaccessthenecessarysymbolsspanaccess-the-necessary-symbols"></a><span id="access_the_necessary_symbols"></span><span id="ACCESS_THE_NECESSARY_SYMBOLS"></span>访问必需的符号

在使用之前 UMDH，必须为应用程序具有访问正确的符号。 UMDH 使用环境变量指定的符号路径\_NT\_符号\_路径。 设置为包含你的应用程序的符号的路径，此变量等。

如果还包括 Windows 符号的路径，分析可能会更完整。 此符号路径的语法等同于使用的调试器;有关详细信息，请参阅[符号路径](symbol-path.md)。

例如，如果你的应用程序的符号位于 c:\\MyApp\\符号，并且您已安装的 Windows 符号文件\\ \\myshare\\winsymbols，会使用以下若要设置符号路径的命令：

```console
set _NT_SYMBOL_PATH=c:\myapp\symbols;\\myshare\winsymbols
```

再举一例，如果你的应用程序的符号位于 c:\\MyApp\\符号和你想要使用公共 Microsoft 符号存储区的 Windows 符号，使用 c:\\MyCache 作为下游存储，你将使用以下命令设置符号路径：

```console
set _NT_SYMBOL_PATH=c:\myapp\symbols;srv*c:\mycache*https://msdl.microsoft.com/download/symbols
```

**重要**  假设您有两台计算机：*记录计算机*创建 UMDH 日志和一个*分析计算机*分析 UMDH 日志的位置。 分析计算机上的符号路径必须指向日志时间在加载日志记录计算机的 Windows 版本的符号。 未指向符号路径分析计算机上的符号服务器。 如果这样做，UMDH 将检索分析计算机运行的 Windows 版本的符号和 UMDH 将不会显示有意义的结果。

 

### <a name="span-iddisablebstrcachingspanspan-iddisablebstrcachingspandisable-bstr-caching"></a><span id="disable_bstr_caching"></span><span id="DISABLE_BSTR_CACHING"></span>禁用 BSTR 缓存

自动化 （以前称为 OLE 自动化） 缓存的 BSTR 字符串所用的内存。 这可以防止 UMDH 正确确定内存分配的所有者。 若要避免此问题，必须禁用 BSTR 缓存。

若要禁用 BSTR 缓存，请将 OANOCACHE 环境变量设置为一 (1)。 启动其分配是要跟踪的应用程序之前，必须进行此设置。

或者，可以禁用 BSTR 缓存从应用程序本身中通过调用.NET Framework **SetNoOaCache**函数。 如果选择此方法，则应调用此函数早期，因为已被任何 BSTR 分配缓存何时**SetNoOaCache**调用后将保留在缓存。

如果需要跟踪由服务进行的分配，你必须将 OANOCACHE 设置为系统环境变量，然后重新为此设置的 Windows 才会生效。

在 Windows 2000 上除了设置 OANOCACHE 等于 1，您还必须安装随附的修补程序[Microsoft 支持文章 139071](https://go.microsoft.com/fwlink/p/?LinkId=241583)。 在 Windows XP 和更高版本的 Windows 上不需要此修补程序。

### <a name="span-idfindtheprocessidspanspan-idfindtheprocessidspanfind-the-process-id"></a><span id="find_the_process_id"></span><span id="FIND_THE_PROCESS_ID"></span>查找进程 ID

UMDH 标识进程的进程标识符 (PID)。 你可以通过使用任务管理器中，任务列表，查找任何正在运行的进程的 PID 或[TList](tlist.md)。

 

 





