---
title: 启用事后调试
description: 本主题介绍如何启用事后调试
ms.assetid: ae116b60-fed2-4e1d-98a8-9fe83f460c50
keywords: 调试. 调试，Windbg，事后调试，实时调试，JIT 调试，AeDebug 注册表项
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 68aff3f255916d0b36363acb15edf0881de4bb14
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715006"
---
# <a name="enabling-postmortem-debugging"></a>启用事后调试


## <a name="span-idddk_enabling_postmortem_debugging_dbgspanspan-idddk_enabling_postmortem_debugging_dbgspanuser-mode-exception-handling"></a><span id="ddk_enabling_postmortem_debugging_dbg"></span><span id="DDK_ENABLING_POSTMORTEM_DEBUGGING_DBG"></span>用户模式异常处理


**异常和断点**

最常见的应用程序错误称为 "异常"。 其中包括访问冲突、被零除错误、数字溢出、CLR 异常以及许多其他类型的错误。 应用程序还可能导致断点中断。 当 Windows 无法运行应用程序 (例如，无法加载所需的模块时) 或遇到断点时，会出现这种情况。 断点可以由调试器插入到代码中，也可以通过 [**DebugBreak**](/windows/win32/api/debugapi/nf-debugapi-debugbreak)等函数进行调用。

**异常处理程序优先顺序**

Windows 根据配置值以及哪些调试程序处于活动状态，以各种方式处理用户模式错误。 以下序列显示了用于用户模式错误处理的优先级：

1.  如果用户模式调试器当前已附加到出错进程，则所有错误都将导致目标中断此调试器。

    只要附加了用户模式调试器，就不会再使用其他错误处理方法--即使 [**gn (未处理异常) **](gn--gn--go-with-exception-not-handled-.md) 命令。

2.  如果没有附加用户模式调试器，并且执行代码具有其自己的异常处理例程 (例如， **try-except**) ，则此异常处理例程将尝试处理错误。

3.  如果没有附加用户模式调试器，并且 Windows 具有开放内核调试连接，并且错误是断点中断，则 Windows 将尝试联系内核调试器。

    在 Windows 启动过程中，必须打开内核调试连接。 如果希望防止用户模式中断进入内核调试器，可以将 KDbgCtrl 实用工具与 **-du** 参数一起使用。 有关如何配置内核调试连接以及如何使用 KDbgCtrl 的详细信息，请参阅 [获取调试设置](getting-set-up-for-debugging.md)。

    在内核调试器中，您可以使用 [**gh () 处理异常 **](gh--go-with-exception-handled-.md) ，以忽略错误并继续运行目标。 您可以使用 [**gn ("未处理异常") **](gn--gn--go-with-exception-not-handled-.md) ，绕过内核调试器并继续执行步骤4。

4.  如果步骤1、2和3中的条件不适用，Windows 将激活在 AeDebug 注册表值中配置的调试工具。 在此情况下，可以提前选择任何程序作为工具使用。 选择的程序称为 *事后调试器*。

5.  如果步骤1、2和3中的条件不适用，并且未注册事后调试器，则 Windows 错误报告 (WER) 会显示一条消息，并在有任何可用的情况下提供解决方案。 如果在注册表中设置了适当的值，则 WER 还会写入内存转储文件。 有关详细信息，请参阅 [使用 WER](/windows/win32/wer/using-wer) 和 [收集用户模式转储](/windows/win32/wer/collecting-user-mode-dumps)。

**DebugBreak 函数**

如果已安装事后调试器，可以通过调用 **DebugBreak** 函数从用户模式应用程序中有意中断到调试器。

## <a name="span-idspecifying_a_postmortem_debuggerspanspan-idspecifying_a_postmortem_debuggerspanspan-idspecifying_a_postmortem_debuggerspanspecifying-a-postmortem-debugger"></a><span id="Specifying_a_Postmortem_Debugger"></span><span id="specifying_a_postmortem_debugger"></span><span id="SPECIFYING_A_POSTMORTEM_DEBUGGER"></span>指定事后调试器


本部分介绍如何将 WinDbg 等工具配置为事后调试器。 配置后，每当应用程序崩溃时，将自动启动事后调试器。

**Post 事后调试器注册表项**

Windows 错误报告 (WER) 使用在 AeDebug 注册表项中设置的值创建事后调试进程。

**HKLM** \\**软件** \\**Microsoft** \\**WINDOWS NT** \\**CurrentVersion** \\**AeDebug**

有两个重要的主注册表值： " *调试器* " 和 " *自动*"。 *调试器* 注册表值指定事后调试器的命令行。 *自动*注册表值指定是自动启动事后调试器，还是首先显示确认消息框。

<span id="Debugger__REG_SZ_"></span><span id="debugger__reg_sz_"></span><span id="DEBUGGER__REG_SZ_"></span>**调试器 (REG \_ SZ) **  

此 REG \_ SZ 值指定将处理事后调试的调试器。

必须列出调试器的完整路径，除非调试器位于默认路径中的目录中。

命令行是通过包含3个参数的 printf 样式调用从调试器字符串生成的。 尽管顺序是固定的，但不需要使用任何或所有可用参数。

DWORD (% ld) -目标进程的进程 ID。

DWORD (% ld) 事件句柄重复到事后调试进程。 如果事后调试器发出事件信号，则 WER 将继续目标进程，而不会等待事后调试器终止。 只有在问题得到解决后，才应发出事件信号。 如果事后调试器在终止时未发出事件的信号，则 WER 会继续收集有关目标进程的信息。

void \* (% p) - \_ \_ 在目标进程的地址空间中分配的 JIT 调试信息结构的地址。 结构包含其他异常信息和上下文。

<span id="Auto__REG_SZ_"></span><span id="auto__reg_sz_"></span><span id="AUTO__REG_SZ_"></span>**自动 (REG \_SZ) ** 此 REG \_ SZ 值始终是 **0** 或 **1**。

如果 " **自动** " 设置为 **0**，则在开始调试调试过程之前，将显示确认消息框。

如果 " **自动** " 设置为 **1**，则会立即创建 "事后调试程序"。

手动编辑注册表时，请特别小心，因为对注册表所做的更改可能不允许 Windows 启动。

**示例命令行用法**

许多事后调试程序使用命令行（包括-p 和-e 开关）来指示参数分别是 PID 和事件 () 。 例如，通过安装 WinDbg，会 `windbg.exe -I` 创建以下值：

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

可以灵活地使用 WER% ld% ld% p 参数。 例如， 不需要在 WER 参数前后指定任何开关。 例如，使用安装 [Windows Sysinternals ProcDump](/sysinternals/downloads/procdump) 会 `procdump.exe -i` 创建以下值，而不会在 WER% ld% ld% p 参数之间切换：

```console
Debugger = "<Path>\procdump.exe" -accepteula -j "c:\Dumps" %ld %ld %p
Auto = 1
```

**32和64位调试器**

在64位平台上，调试器 (REG \_ sz) 和 Auto (reg \_ sz) 注册表值分别为64位和32位应用程序定义。 Windows 上的其他 Windows (WOW) 键用于存储32位应用程序 post 事后调试值。

**HKLM** \\**软件** \\**Wow6432Node** \\**Microsoft** \\**WINDOWS NT** \\**CurrentVersion** \\**AeDebug**

在64位平台上，为32位进程使用32位事后调试器，为64位进程使用64位调试器。 这样就避免了64位调试程序，它将精力集中在 WOW64 线程上，而不是32位线程的32位进程中。

对于许多事后调试程序，包括用于 Windows 的调试工具事后调试器，这涉及到运行安装命令两次;一次是 x86 版本，一次是 x64 版本。 例如，若要使用 WinDbg 作为交互式的事后调试，则该命令将为 `windbg.exe -I` 每个版本运行两次。

64位安装：

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
```

这会用这些值更新注册表项。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -p %ld -e %ld –g
```

32位安装：

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

这会用这些值更新注册表项。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe" -p %ld -e %ld –g
```

## <a name="span-idconfiguringspanspan-idconfiguringspanspan-idconfiguringspanconfiguring-post-mortem-debuggers"></a><span id="Configuring"></span><span id="configuring"></span><span id="CONFIGURING"></span>配置 Post 事后调试器


### <a name="span-iddebugging_tools_for_windowsspanspan-iddebugging_tools_for_windowsspanspan-iddebugging_tools_for_windowsspandebugging-tools-for-windows"></a><span id="Debugging_Tools_for_Windows"></span><span id="debugging_tools_for_windows"></span><span id="DEBUGGING_TOOLS_FOR_WINDOWS"></span>适用于 Windows 的调试工具

Windows 调试器的调试工具都支持将设置为事后调试器。 安装命令旨在以交互方式调试进程。

**WinDbg**

若要将事后调试器设置为 WinDbg，请运行 `windbg -I` 。  (`I` 必须大写。 ) 此命令在使用后将显示成功或失败消息。 若要使用32和64位应用程序，请对64和32调试器运行命令。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

这是运行时将如何配置 AeDebug 注册表项 `windbg -I` 。

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

在示例中， * &lt; Path &gt; *是调试程序所在的目录。

如前文所述，-p 和-e 参数传递了进程 ID 和事件。

**-G**将 g (中转) 命令传递给 WinDbg，并继续执行当前指令。

**注意**   传递 g (中转) 命令时出现重大问题。 此方法的问题是，异常并不总是重复，这通常是由于在重新启动代码时不再存在的暂时情况。 有关此问题的详细信息，请参阅 [**。 jdinfo (使用 JIT \_ 调试 \_ 信息) **](-jdinfo--use-jit-debug-info-.md)。

若要避免此问题，请使用 jdinfo 或/j.。 此方法允许调试器位于相关代码失败的上下文中。 有关详细信息，请参阅本主题后面的实时 [ (JIT) 调试](#jit) 。

 

**CDB**

若要将事后调试器设置为 CDB，请运行 **cdb-iae** (Install AeDebug) 或 **CDB-Iaec** *KeyString* (install AeDebug with Command) 。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iae
```

使用 **-iaec** 参数时， *KeyString* 指定要追加到命令行末尾的字符串，该命令行用于启动事后调试调试器。 如果 *KeyString* 包含空格，则必须用引号将其引起来。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iaec [KeyString]
```

如果此命令成功，则不显示任何内容，如果失败，则显示错误消息。

**NTSD**

若要将事后调试器设置为 NTSD，请运行 **ntsd-iae** (install AeDebug) 或 **NTSD Iaec** *KeyString* (install AeDebug with Command) 。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iae
```

使用 **-iaec** 参数时， *KeyString* 指定要追加到命令行末尾的字符串，该命令行用于启动事后调试调试器。 如果 *KeyString* 包含空格，则必须用引号将其引起来。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iaec [KeyString]
```

如果此命令成功，则不显示任何内容，并在出现故障时显示新的控制台窗口。

**注意**   由于-p% ld-e% ld-g 参数总是首先出现在事后调试器的命令行上，因此不应使用-iaec 开关来指定-server 参数，因为-server 在命令行上首先显示时将无法工作。 若要安装包含此参数的事后调试器，必须手动编辑注册表。

 

### <a name="span-idvisual_studio_jit_debuggerspanspan-idvisual_studio_jit_debuggerspanspan-idvisual_studio_jit_debuggerspanvisual-studio-jit-debugger"></a><span id="Visual_Studio_JIT_Debugger"></span><span id="visual_studio_jit_debugger"></span><span id="VISUAL_STUDIO_JIT_DEBUGGER"></span>Visual Studio JIT 调试器

如果已安装 Visual Studio，vsjitdebugger.exe 将注册为 post 事后调试器。 Visual Studio JIT 调试器打算以交互方式调试进程。

```console
Debugger = "C:\WINDOWS\system32\vsjitdebugger.exe" -p %ld -e %ld
```

如果更新或重新安装了 Visual Studio，则会重新写入此项，并覆盖所有替换值集。

### <a name="span-idwindow_sysinternals_procdumpspanspan-idwindow_sysinternals_procdumpspanspan-idwindow_sysinternals_procdumpspanwindow-sysinternals-procdump"></a><span id="Window_Sysinternals_ProcDump"></span><span id="window_sysinternals_procdump"></span><span id="WINDOW_SYSINTERNALS_PROCDUMP"></span>Window Sysinternals ProcDump

Windows Sysinternals ProcDump 实用程序还可用于事后转储捕获。 有关使用和下载 ProcDump 的详细信息，请参阅 [ProcDump](/sysinternals/downloads/procdump)。

与 [**dump**](-dump--create-dump-file-.md) WinDbg 命令一样，ProcDump 能够以非交互方式捕获崩溃转储。 捕获可能出现在任何 Windows 系统会话中。

当转储文件捕获完成时，ProcDump 将退出，然后，WER 会报告失败，错误过程将终止。

使用 `procdump -i` 安装 procdump 和-对于32和64位 post 事后调试，同时卸载 procdump。

```console
<Path>\procdump.exe -i
```

安装和卸载命令输出成功时修改的注册表值以及失败时的错误。

注册表中的 ProcDump 命令行选项设置为：

```console
Debugger = <Path>\ProcDump.exe -accepteula -j "<DumpFolder>" %ld %ld %p
```

ProcDump 使用所有3个参数-PID、事件和 JIT \_ 调试 \_ 信息。 有关 JIT \_ 调试信息参数的详细信息 \_ ，请参阅下面的实时 [ (JIT) 调试](#jit) 。

捕获的转储大小默认为迷你 (进程/线程/句柄/模块/地址空间) ，无需大小的选项集，小型增强 (小型加 \_ 内存专用页) 使用-mp 集，或完全 (与-mA 集 ) 的所有内存等效于 "/mA"。

对于驱动器空间充足的系统，建议使用完全 () 捕获。

使用带有-i 选项的-ma 指定所有内存捕获。 还可以提供转储文件的路径。

```console
<Path>\procdump.exe -ma -i c:\Dumps
```

对于驱动器空间有限的系统，建议使用小型增强 ( mp) 捕获。

```console
<Path>\procdump.exe -mp -i c:\Dumps
```

要将转储文件保存到的文件夹是可选的。 默认值为当前文件夹。 应使用与用于 C： Windows Temp 相同或更好的 ACL 来保护文件夹 \\ \\ 。有关管理与文件夹相关的安全性的详细信息，请参阅 [事后调试过程中的安全性](security-during-postmortem-debugging.md)。

若要将 ProcDump 卸载为事后调试器，并还原以前的设置，请使用-u (卸载) 选项。

```console
<Path>\procdump.exe -u
```

"安装" 和 "卸载" 命令在64位平台上设置64位和32位值。

ProcDump 是一个 "打包" 的可执行文件，其中包含应用程序的32位和64位版本，这同样适用于32位和64位。 当 ProcDump 运行时，如果运行的版本不匹配目标进程，它将自动切换版本。

## <a name="span-idjitspanspan-idjitspan-just-in-time-jit-debugging"></a><span id="JIT"></span><span id="jit"></span> 实时 (JIT) 调试


**设置出错应用程序的上下文**

如前文所述，使用 JIT \_ 调试信息参数将上下文设置为导致崩溃的异常非常有必要 \_ 。 有关此内容的详细信息，请参阅 [**。 jdinfo (使用 JIT \_ 调试 \_ 信息) **](-jdinfo--use-jit-debug-info-.md)。

**Windows 调试工具**

此示例显示了如何编辑注册表以运行 (-c) 的初始命令，该命令使用. jdinfo &lt; address &gt; 命令显示其他异常信息，并将上下文更改为异常的位置 (类似于使用 ecxr。将上下文设置为异常记录) 。

```console
Debugger = "<Path>\windbg.exe -p %ld -e %ld -c ".jdinfo 0x%p"
Auto = 1
```

% P 参数是 \_ \_ 目标进程的地址空间中的 JIT 调试信息结构的地址。 % P 参数使用0x 预先追加，以便将其解释为十六进制值。 有关详细信息，请参阅 [**。 jdinfo (使用 JIT \_ 调试 \_ 信息) **](-jdinfo--use-jit-debug-info-.md)。

若要调试32和64位应用的组合，请配置 (以上所述) 的32和64位注册表项，并将正确的路径设置为64位和 32 WinDbg.exe 的位置。

**使用转储创建转储文件**

若要在出现包含 JIT 调试信息数据的故障时捕获转储文件 \_ \_ ，请使用. dump/j &lt; address &gt; 。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd"
```

使用/u 选项生成唯一的文件名，以允许自动创建多个转储文件。 有关选项的详细信息，请参阅 [**。 dump (创建转储文件) **](-dump--create-dump-file-.md)。

创建的转储会将 JITDEBUG \_ 信息数据存储为默认的异常上下文。 请使用 .exr-1 显示异常记录和 ecxr，以设置上下文，而不是使用 jdinfo 查看异常信息和设置上下文。 有关详细信息，请参阅 [**。 .exr (显示异常记录) **](-exr--display-exception-record-.md) 和 [**. Ecxr () 显示异常上下文记录 **](-ecxr--display-exception-context-record-.md)。

**Windows 错误报告-q/qd**

调试会话结束的方式决定 Windows 错误报告是否报告失败。

如果在关闭调试器之前使用 qd 分离调试会话，则 WER 将报告失败。

如果使用 q (退出调试会话，或者如果在未分离) 的情况下关闭调试器，则 WER 不会报告失败。

将 *; q* 或 *; qd* 追加到命令字符串的末尾，以调用所需的行为。

例如，若要允许 WER 在 CDB 捕获转储后报告失败，请配置此命令字符串。

```console
<Path>\cdb.exe -p %ld -e %ld -c ".dump /j 0x%p /u c:\Dumps\AeDebug.dmp; qd"
```

此示例将允许 WER 在 WinDbg 捕获转储后报告故障。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd""
```

## <a name="span-idsecurity_vulnerabilitiesspanspan-idsecurity_vulnerabilitiesspansecurity-vulnerabilities"></a><span id="security_vulnerabilities"></span><span id="SECURITY_VULNERABILITIES"></span>安全漏洞


如果考虑在与他人共享的计算机上启用事后调试，请参阅 [事后调试过程中的安全性](security-during-postmortem-debugging.md)。

 

