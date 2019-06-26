---
title: 启用事后调试
description: 本主题介绍如何启用事后调试
ms.assetid: ae116b60-fed2-4e1d-98a8-9fe83f460c50
keywords: 调试。 调试，Windbg，事后调试、 在实时调试、 JIT 调试、 AeDebug 注册表项
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: cb3b9dfa53ae3ef7a615f1586a1ed92ba0a585be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361385"
---
# <a name="enabling-postmortem-debugging"></a>启用事后调试


## <a name="span-idddkenablingpostmortemdebuggingdbgspanspan-idddkenablingpostmortemdebuggingdbgspanuser-mode-exception-handling"></a><span id="ddk_enabling_postmortem_debugging_dbg"></span><span id="DDK_ENABLING_POSTMORTEM_DEBUGGING_DBG"></span>用户模式异常处理


**异常和断点**

最常见的应用程序错误称为异常。 其中包括访问冲突、 被零除错误、 出现了数值溢出、 CLR 异常和许多其他类型的错误。 应用程序也会导致断点中断。 当 Windows 无法运行 （例如，无法加载必需的模块时） 应用程序时或当遇到断点时，会发生这些问题。 可以插入到代码中由调试器，断点或如函数通过调用[ **DebugBreak**](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-debugbreak)。

**异常处理程序优先顺序**

Windows 基于配置值和哪些调试器处于活动状态，处理用户模式下的错误中有许多种。 按以下顺序显示了用于用户模式下的错误处理的优先顺序：

1.  如果用户模式下调试器当前附加到错误的进程，所有错误将都导致要在此调试器中中断的目标。

    只要用户模式下调试器已附加，则将使用没有其他错误处理的方法-即使[ **gn （Go 与未处理异常）** ](gn--gn--go-with-exception-not-handled-.md)使用命令。

2.  如果没有用户模式下调试器已附加，并执行代码具有其自己的异常处理例程 (例如，**试用-除**)，此异常处理例程将尝试处理的错误。

3.  如果未用户模式下附加调试器，以及 Windows 已打开的内核调试连接，并且错误发生断点中断，则 Windows 将尝试联系内核调试程序。

    在 Windows 的启动过程中，必须打开的内核调试连接。 如果你想要阻止的用户模式下中断分解为内核调试程序，则可以使用 KDbgCtrl 实用程序用于 **-du**参数。 有关如何配置内核调试连接以及如何使用 KDbgCtrl 的详细信息，请参阅[获取设置以便进行调试](getting-set-up-for-debugging.md)。

    在内核调试器中，你可以使用[ **（请使用异常处理） 的 gh** ](gh--go-with-exception-handled-.md)忽略错误并继续运行目标。 可以使用[ **gn （Go 与未处理异常）** ](gn--gn--go-with-exception-not-handled-.md)要绕过内核调试程序，并继续到步骤 4。

4.  如果在步骤 1、 2 和 3 中的条件不适用，则 Windows 将激活 AeDebug 注册表值中配置的调试工具。 任何程序可以选择提前为工具在此情况下使用。 所选的程序被称为*事后调试器*。

5.  如果在步骤 1、 2 和 3 中的条件不适用，并且没有任何事后调试器注册，Windows 错误报告 (WER) 将显示一条消息，并提供解决方案，如果有的话。 WER 还写入内存转储文件在注册表中设置相应的值。 有关详细信息，请参阅[使用 WER](https://go.microsoft.com/fwlink/p?LinkID=257799)并[收集用户模式转储](https://go.microsoft.com/fwlink/p?LinkID=257798)。

**DebugBreak 函数**

如果已安装事后调试器，您可以故意中断调试器从用户模式应用程序通过调用**DebugBreak**函数。

## <a name="span-idspecifyingapostmortemdebuggerspanspan-idspecifyingapostmortemdebuggerspanspan-idspecifyingapostmortemdebuggerspanspecifying-a-postmortem-debugger"></a><span id="Specifying_a_Postmortem_Debugger"></span><span id="specifying_a_postmortem_debugger"></span><span id="SPECIFYING_A_POSTMORTEM_DEBUGGER"></span>指定事后调试器


本部分介绍如何将 WinDbg 之类的工具配置为在事后调试器。 配置后，每当应用程序崩溃时，会自动启动事后调试器。

**Post Mortem 调试器注册表项**

Windows 错误报告 (WER) 创建事后调试器进程使用 AeDebug 注册表项中设置的值。

**HKLM**\\**软件**\\**Microsoft**\\**Windows NT** \\ **CurrentVersion**\\**AeDebug**

有两个主要的注册表值的感兴趣，*调试器*并*自动*。*调试器*注册表值指定事后调试程序命令行。 *自动*注册表值指定如果事后调试器自动启动，或首先会出现一个确认消息框。

<span id="Debugger__REG_SZ_"></span><span id="debugger__reg_sz_"></span><span id="DEBUGGER__REG_SZ_"></span>**调试器 (REG\_SZ)**  

此 REG\_SZ 值指定将处理事后调试的调试程序。

必须列出到调试器的完整路径，除非调试器位于默认路径中的目录中。

命令行从通过包括 3 个参数的 printf 样式调用调试器字符串生成。 尽管顺序固定的但并不要求使用任何或所有可用参数。

DWORD (%ld) 的目标进程的进程 ID。

DWORD (%ld) 的事件处理复制到事后调试器进程。 如果事后调试器向事件发出信号，WER 将继续而不等待事后调试程序终止的目标进程。 该事件应仅用信号通知是否已解决此问题。 如果事后调试器终止而未发出事件信号，WER 将继续目标进程的信息的集合。

void\* (%p) 的地址的 JIT\_调试\_分配目标进程的地址空间中的信息结构。 该结构包含其他异常信息和上下文。

<span id="Auto__REG_SZ_"></span><span id="auto__reg_sz_"></span><span id="AUTO__REG_SZ_"></span>**自动 (REG\_SZ)** 此 REG\_SZ 值始终是任一**0**或**1**。

如果**自动**设置为**0**，在事后调试的进程正在启动之前显示确认消息框。

如果**自动**设置为**1**，事后调试器立即创建。

当你手动编辑注册表时，执行起来非常，由于对注册表的不正确更改可能不允许 Windows 启动。

**示例命令行用法**

许多事后调试器使用命令行包含-p 和-e 开关来指示参数分别是 PID 和事件。 例如，安装通过 WinDbg`windbg.exe -I`创建以下值：

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

如何使用 WER %ld%ld %p 参数处于大的灵活性。 举个例子。 没有无需指定任何开关或 WER 参数之间。 例如，安装[Windows Sysinternals ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)使用`procdump.exe -i`不带任何开关之间 WER %ld%ld %p 参数创建以下值：

```console
Debugger = "<Path>\procdump.exe" -accepteula -j "c:\Dumps" %ld %ld %p
Auto = 1
```

**32 位和 64 位的调试器**

在 64 位平台上，调试器 (REG\_SZ) 和自动 (REG\_SZ) 注册表值单独定义的 64 位和 32 位应用程序。 其他 Windows Windows (WOW) 项上的用于存储 32 位应用程序 post mortem 调试值。

**HKLM**\\**软件**\\**Wow6432Node**\\**Microsoft** \\ **Windows NT**\\**CurrentVersion**\\**AeDebug**

在 64 位平台上，对于 32 位进程和 64 位调试程序的 64 位进程中使用 32 位的事后调试程序。 这样可避免 64 位调试程序将重点放在 WOW64 线程，而不是 32 位线程，在 32 位进程中。

对于许多事后调试器，包括有关 Windows 调试工具事后调试程序，这涉及到运行安装命令两次;一次与 x86 版本，一次用于 x64 版本。 例如，若要为交互式的事后调试程序，使用 WinDbg`windbg.exe -I`命令会运行两次，一次为每个版本。

64 位安装：

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
```

这会使用这些值更新注册表项。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -p %ld -e %ld –g
```

32 位安装：

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

这会使用这些值更新注册表项。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe" -p %ld -e %ld –g
```

## <a name="span-idconfiguringspanspan-idconfiguringspanspan-idconfiguringspanconfiguring-post-mortem-debuggers"></a><span id="Configuring"></span><span id="configuring"></span><span id="CONFIGURING"></span>配置 Post Mortem 调试器


### <a name="span-iddebuggingtoolsforwindowsspanspan-iddebuggingtoolsforwindowsspanspan-iddebuggingtoolsforwindowsspandebugging-tools-for-windows"></a><span id="Debugging_Tools_for_Windows"></span><span id="debugging_tools_for_windows"></span><span id="DEBUGGING_TOOLS_FOR_WINDOWS"></span>有关 Windows 调试工具

调试工具的 Windows 调试器设置为事后调试程序的所有支持。 安装命令想要以交互方式调试该进程。

**WinDbg**

若要设置为 WinDbg 事后调试器，运行`windbg -I`。 (`I`必须采用大写形式。)在使用后，此命令将显示成功或失败消息。 若要使用 32 位和 64 位应用程序，请为这两个 64 和 32 调试器中运行命令。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

这是将进行 AeDebug 注册表项的方式配置时`windbg -I`运行。

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

在示例中， *&lt;路径&gt;* 是调试器所在的目录。

-P 和-e 参数传递进程 ID 和事件，如前面所述。

**-G**将 g （转到） 命令传递给 WinDbg 和继续从当前指令的执行。

**请注意**  传递 g （转到） 命令的一个重要问题。 使用此方法时，问题是，异常不始终会重复，通常情况下，由于临时性条件不再存在时重新启动代码。 有关此问题的详细信息，请参阅[ **.jdinfo (使用 JIT\_调试\_信息)** ](-jdinfo--use-jit-debug-info-.md)。

若要避免此问题，请使用.jdinfo 或.dump /j。 这种方法使调试器处于感兴趣的代码失败的上下文。 有关详细信息，请参阅[实时 (JIT) 调试](#jit)本主题中更高版本。

 

**CDB**

若要设置为 CDB 事后调试器，运行**cdb iae** (安装 AeDebug) 或**cdb iaec** *KeyString* (使用命令，安装 AeDebug)。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iae
```

当 **-iaec**使用参数，则*KeyString*指定要追加到用来启动事后调试程序命令行末尾的字符串。 如果*KeyString*包含空格，则必须用引号引起来。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iaec [KeyString]
```

如果失败，此命令显示 nothing 如果成功，和一条错误消息。

**NTSD**

若要设置为 NTSD 事后调试器，运行**ntsd iae** (安装 AeDebug) 或**ntsd iaec** *KeyString* (使用命令，安装 AeDebug)。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iae
```

当 **-iaec**使用参数，则*KeyString*指定要追加到用来启动事后调试程序命令行末尾的字符串。 如果*KeyString*包含空格，则必须用引号引起来。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iaec [KeyString]
```

此命令显示到新的控制台窗口在失败时执行任何操作如果成功，而是一个错误。

**请注意**  -p %ld-e %ld-g 参数始终的事后调试程序命令行中第一个显示，因为您不应该使用-iaec 开关来指定-server 参数因为-服务器不会起作用，除非它出现在第一个命令行中。 若要安装的事后调试程序包括此参数，则必须手动编辑注册表。

 

### <a name="span-idvisualstudiojitdebuggerspanspan-idvisualstudiojitdebuggerspanspan-idvisualstudiojitdebuggerspanvisual-studio-jit-debugger"></a><span id="Visual_Studio_JIT_Debugger"></span><span id="visual_studio_jit_debugger"></span><span id="VISUAL_STUDIO_JIT_DEBUGGER"></span>Visual Studio JIT 调试器

如果已安装 Visual Studio，vsjitdebugger.exe 将注册为 post mortem 调试器。 Visual Studio JIT 调试器想要以交互方式调试该进程。

```console
Debugger = "C:\WINDOWS\system32\vsjitdebugger.exe" -p %ld -e %ld
```

如果更新或重新安装 Visual Studio，则此条目将经过重新编写，覆盖任何备用值集。

### <a name="span-idwindowsysinternalsprocdumpspanspan-idwindowsysinternalsprocdumpspanspan-idwindowsysinternalsprocdumpspanwindow-sysinternals-procdump"></a><span id="Window_Sysinternals_ProcDump"></span><span id="window_sysinternals_procdump"></span><span id="WINDOW_SYSINTERNALS_PROCDUMP"></span>窗口 Sysinternals ProcDump

Windows Sysinternals ProcDump 实用工具还可以用于事后转储捕获。 有关使用和下载 ProcDump 的详细信息，请参阅[ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) TechNet 上。

像[ **.dump** ](-dump--create-dump-file-.md) WinDbg 命令中，ProcDump 为能够被捕获的崩溃转储以非交互方式。 捕获可能会出现在任何 Windows 系统会话中。

ProcDump 退出时转储文件捕获完成后，WER，然后将报告失败并出错进程将终止。

使用`procdump -i`procdump 和-您需要卸载 ProcDump，两个 post mortem 调试的 32 位和 64 位安装。

```console
<Path>\procdump.exe -i
```

安装和卸载的注册表值已修改成功和失败的错误的命令输出。

在注册表中的 ProcDump 命令行选项设置为：

```console
Debugger = <Path>\ProcDump.exe -accepteula -j "<DumpFolder>" %ld %ld %p
```

ProcDump 使用所有 3 个参数-PID、 事件和 JIT\_调试\_信息。 有关详细信息，JIT\_调试\_信息参数，请参阅[实时 (JIT) 调试](#jit)下面。

转储大小捕获而无需大小的选项集，MiniPlus 与 Mini （进程/线程/句柄/模块/地址空间） 的默认值 (加上内存优化的最小\_专用页)-mp 集或填满 （所有内存-等效于".dump /mA"）-ma 设置。

对于具有足够的驱动器空间，完整的系统 (-ma) 建议捕获。

使用-ma 与-i 选项来指定所有的内存捕获。 （可选） 提供的转储文件的路径。

```console
<Path>\procdump.exe -ma -i c:\Dumps
```

对于具有有限的驱动器空间，小型增强系统 (-mp) 建议捕获。

```console
<Path>\procdump.exe -mp -i c:\Dumps
```

若要保存的转储文件的文件夹是可选的。 默认值为当前文件夹。 该文件夹应使用等于或优于 c： 使用 ACL 保护\\Windows\\Temp。有关管理安全与文件夹相关的详细信息，请参阅[安全在事后调试](security-during-postmortem-debugging.md)。

若要卸载 ProcDump 作为事后调试程序，并还原以前的设置，请使用-u （卸载） 选项。

```console
<Path>\procdump.exe -u
```

安装和卸载这两个 64 位和 32 位值在 64 位平台上的命令集。

ProcDump"打包"包含的 32 位和 64 位版本的应用程序-这种情况下都可执行文件，同一可执行文件用于 32 位和 64 位。 ProcDump 运行时，它会自动切换版本，如果运行的版本与目标进程不匹配。

## <a name="span-idjitspanspan-idjitspan-just-in-time-jit-debugging"></a><span id="JIT"></span><span id="jit"></span> 只需在实时 (JIT) 调试


**将上下文设置为出错的应用程序**

如前文所述，它是非常可取，以将上下文设置为导致使用 JIT 发生故障的异常\_调试\_信息参数。 有关详细信息，请参阅[ **.jdinfo (使用 JIT\_调试\_信息)** ](-jdinfo--use-jit-debug-info-.md)。

**Windows 调试工具**

此示例演示如何编辑注册表以运行初始命令 (-c)，它使用.jdinfo&lt;地址&gt;命令以显示其他异常信息，并将上下文更改为 （类似于如何异常的位置。使用 ecxr 将上下文设置为异常记录)。

```console
Debugger = "<Path>\windbg.exe -p %ld -e %ld -c ".jdinfo 0x%p"
Auto = 1
```

%P 参数是 JIT 的地址\_调试\_目标进程的地址空间中的信息结构。 %P 参数预追加 0x，以便将解释为十六进制值。 有关详细信息，请参阅[ **.jdinfo (使用 JIT\_调试\_信息)** ](-jdinfo--use-jit-debug-info-.md)。

若要调试的 32 位和 64 位应用程序混合在一起，配置两个 32 位和 64 位注册表项 （如上所述），将正确的路径设置为 64 位和 32 位 WinDbg.exe 的位置。

**创建使用.dump 转储文件**

若要捕获的转储文件失败时，包括 JIT\_调试\_信息数据，请使用.dump /j&lt;地址&gt;。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd"
```

/U 选项用于生成唯一文件名以允许多个转储文件会自动创建。 有关选项，请参阅详细信息[ **.dump （创建转储文件）** ](-dump--create-dump-file-.md)。

创建的转储会 JITDEBUG\_信息数据存储为默认异常上下文。 而不是使用.jdinfo 查看异常信息和设置上下文，使用.exr-1 来显示异常记录和.ecxr 设置上下文。 有关详细信息请参阅[ **.exr （显示异常记录）** ](-exr--display-exception-record-.md)并[ **.ecxr （显示异常上下文记录）** ](-ecxr--display-exception-context-record-.md)。

**Windows 错误报告-q / qd**

方式调试会话结束决定是否 Windows 错误报告报告的失败。

如果使用 qd 在调试器的结束之前分离调试会话时，WER 将报告失败。

如果在调试会话停止使用 q （或如果调试器已关闭而无需分离），请 WER 将不会报告失败。

追加 *; q*或 *; qd*到要调用所需的行为的命令字符串的末尾。

例如，若要允许 WER 后 CDB 捕获转储报告此故障，请配置此命令字符串。

```console
<Path>\cdb.exe -p %ld -e %ld -c ".dump /j 0x%p /u c:\Dumps\AeDebug.dmp; qd"
```

此示例将允许 WER 后 WinDbg 捕获转储报告失败。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd""
```

## <a name="span-idsecurityvulnerabilitiesspanspan-idsecurityvulnerabilitiesspansecurity-vulnerabilities"></a><span id="security_vulnerabilities"></span><span id="SECURITY_VULNERABILITIES"></span>安全漏洞


如果你正在考虑启用事后调试与其他人共享的计算机上，请参阅[安全在事后调试](security-during-postmortem-debugging.md)。

 

 





