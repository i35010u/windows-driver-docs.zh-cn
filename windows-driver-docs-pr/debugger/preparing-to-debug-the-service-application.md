---
title: 准备调试服务应用程序
description: 准备调试服务应用程序
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1588d418f03ae83dc70475771a30068d81f9d3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793242"
---
# <a name="preparing-to-debug-the-service-application"></a>准备调试服务应用程序


本主题列出了调试服务应用程序之前可能需要执行的所有预备步骤。 方案中所需的步骤取决于所选的附加选项以及所选的调试配置。 有关这些选项的列表，请参阅 [选择最佳方法](choosing-the-best-method.md)。

本主题中所述的每个准备步骤均指定了所需的条件。 可以按任意顺序执行这些步骤。

### <a name="span-idenabling-the-debugging-of-the-initialization_codespanspan-idenabling_the_debugging_of_the_initialization_codespan-enabling-the-debugging-of-the-initialization-code"></a><span id="enabling-the-debugging-of-the-initialization_code"></span><span id="ENABLING_THE_DEBUGGING_OF_THE_INITIALIZATION_CODE"></span> 启用初始化代码调试

如果计划从执行开始时调试服务应用程序（包括其初始化代码），则需要此准备步骤。

找到或创建以下注册表项，其中 *ProgramName* 是服务应用程序的可执行文件的名称：

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\ProgramName 
```

*ProgramName* 应包含文件扩展名，而不是路径。 例如， *ProgramName* 可能 Myservice.exe 或 Thisservice.dll。

在此注册表项下，创建一个名为 " **调试器**" 的字符串数据值。 此字符串的值应设置为要附加到服务应用程序的调试程序的完整路径和文件名。

-   如果打算本地调试，请使用如下所示的字符串：

    ```console
    c:\Debuggers\windbg.exe 
    ```

    如果你运行的是 Windows Vista 或更高版本的 Windows，请不要选择此选项。

-   如果计划使用远程调试，请使用-noio 选项指定 NTSD。 这会导致 NTSD 在不使用任何控制台的情况下运行，只能通过远程连接访问。 例如：

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -noio -y SymbolPath 
    ```

    如果调试会话在 Windows 完全加载之前开始，则您可能无法从远程共享访问符号;在这种情况下，必须使用本地符号。 *ServerTransport* 必须指定 Windows 内核实现的传输协议，而不会与用户模式服务（如 TCP 或 NPIPE）进行交互。 有关 *ServerTransport* 的语法，请参阅 [**激活调试服务器**](activating-a-debugging-server.md)。

-   如果计划从内核模式调试器控制用户模式调试器，请使用-d 选项指定 NTSD。 例如：

    ```console
    c:\Debuggers\ntsd.exe -d -y SymbolPath 
    ```

    如果计划使用此方法，并且将从符号服务器访问用户模式符号，则应将此方法与远程调试结合使用。 在这种情况下，请通过-ddefer 选项指定 NTSD。 选择不与用户模式服务（如 TCP 或 NPIPE）交互的 Windows 内核实现的传输协议。 例如：

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -ddefer -y SymbolPath 
    ```

    有关详细信息，请参阅 [从内核调试器控制 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

完成此注册表编辑后，只要启动或重新启动了具有此名称的服务，就会启动调试器。

### <a name="span-idenabling-the-service-application-to-break-into-the-debuggerspanspan-idenabling_the_service_application_to_break_into_the_debuggerspan-enabling-the-service-application-to-break-into-the-debugger"></a><span id="enabling-the-service-application-to-break-into-the-debugger"></span><span id="ENABLING_THE_SERVICE_APPLICATION_TO_BREAK_INTO_THE_DEBUGGER"></span> 使服务应用程序可以中断到调试器

如果希望服务应用程序在崩溃或遇到异常时进入调试器，则需要此准备步骤。 如果要服务应用程序通过调用 **DebugBreak** 函数进入调试器，还需要执行此步骤。

**注意**   如果已启用初始化代码调试 ("启用初始化代码调试" 一节中所述的步骤 ) ，则应跳过此步骤。 启用初始化代码调试后，调试器将在启动时附加到服务应用程序，这会导致所有崩溃、异常和对 **DebugBreak** 的调用都路由到调试器，无需额外的准备工作。

 

此准备步骤涉及到将选择的调试器注册为事后调试器。 这是通过在调试程序命令行上使用-iae 或-iaec 选项来完成的。 建议采用以下命令，但如果要改变它们，请参阅 [启用事后调试](enabling-postmortem-debugging.md)中的语法详细信息。

-   如果打算本地调试，请使用如下所示的命令：

    ```console
    windbg -iae 
    ```

    如果你运行的是 Windows Vista 或更高版本的 Windows，请不要选择此选项。

-   如果计划使用远程调试，请使用-noio 选项指定 NTSD。 这会导致 NTSD 在不使用任何控制台的情况下运行，只能通过远程连接访问。 若要安装包含-server 参数的事后调试器，必须手动编辑注册表;有关详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。 例如， **AeDebug** 键的 **调试器** 值可以是以下值：

    ```console
    ntsd -server npipe:pipe=myproc%x -noio -p %ld -e %ld -g -y SymbolPath 
    ```

    在管道规范中， **% x** 标记替换为启动调试器的进程的进程 ID。 这可以确保如果有多个进程启动事后调试程序，则每个进程都具有唯一的管道名称。 如果调试会话在 Windows 完全加载之前开始，则您可能无法从远程共享访问符号;在这种情况下，必须使用本地符号。 *ServerTransport* 必须指定 Windows 内核实现的传输协议，而不会与用户模式服务（如 TCP 或 NPIPE）进行交互。 有关 *ServerTransport* 的语法，请参阅 [**激活调试服务器**](activating-a-debugging-server.md)。

-   如果计划从内核模式调试器控制用户模式调试器，请使用-d 选项指定 NTSD。 例如：

    ```console
    ntsd -iaec -d -y SymbolPath 
    ```

    如果选择此方法并想要从符号服务器访问用户模式符号，则应将此方法与远程调试结合使用。 在这种情况下，请通过-ddefer 选项指定 NTSD。 选择不与用户模式服务（如 TCP 或 NPIPE）交互的 Windows 内核实现的传输协议。 若要安装包含-server 参数的事后调试器，必须手动编辑注册表;有关详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。 例如， **AeDebug** 键的 **调试器** 值可以是以下值：

    ```console
    ntsd -server npipe:pipe=myproc%x -ddefer -p %ld -e %ld -g -y SymbolPath 
    ```

    有关详细信息，请参阅 [从内核调试器控制 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

发出这些命令之一时，会注册事后调试器。 只要任何用户模式程序（包括服务应用程序）遇到异常或运行 **DebugBreak** 函数，就会启动此调试器。

### <a name="span-idadjusting-the-service-application-timeoutspanspan-idadjusting_the_service_application_timeoutspan-adjusting-the-service-application-timeout"></a><span id="adjusting-the-service-application-timeout"></span><span id="ADJUSTING_THE_SERVICE_APPLICATION_TIMEOUT"></span> 调整服务应用程序超时

如果计划在服务启动时或遇到) 异常时自动启动调试器 (，则需要此准备步骤。

找到以下注册表项：

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control
```

在此项下，找到或创建一个名为 **ServicesPipeTimeout** 的 DWORD 数据值。 将此项设置为你希望服务在超时之前等待的时间量（以毫秒为单位）。例如，值为60000，值为86400000为24小时。 如果未设置此注册表值，则默认超时约为30秒。

此值的意义在于，当启动每个服务时，时钟开始运行，当达到超时值时，附加到服务的任何调试器都将终止。 因此，您选择的值应该比启动服务和完成调试会话之间的总时间要长。

此设置适用于注册表编辑完成后启动或重新启动的每个服务。 如果某些服务崩溃或挂起并且此设置仍然有效，则 Windows 不会检测到此问题。 因此，只应在调试时使用此设置，并在调试完成后将注册表项返回到其原始值。

### <a name="span-idisolating-the-servicespanspan-idisolating_the_servicespan-isolating-the-service"></a><span id="isolating-the-service"></span><span id="ISOLATING_THE_SERVICE"></span> 隔离服务

有时，将多个服务组合到 (Svchost) 进程的单个服务主机中。 如果要调试此类服务，必须首先将其隔离到单独的 Svchost 进程。

可以通过三种方法来隔离服务。 Microsoft 建议将服务移到其自身的组方法，如下所示。 更改服务类型和复制 SvcHost 二进制) 文件 (的替代方法可以暂时用于调试，但由于它们会改变服务的运行方式，因此它们不像第一种方法那样可靠。

**首选方法：将服务移到其自己的组**

1.  发出以下服务配置工具 ( # A0) 命令，其中 *ServiceName* 是服务的名称：

    ```console
    sc qc ServiceName 
    ```

    这会显示服务的当前配置值。 相关值是二进制 \_ 路径名 \_ ，它指定用于启动服务控制程序的命令行。 在这种情况下，由于你的服务尚未隔离，因此此命令行包括一个目录路径、Svchost.exe 和一些 SvcHost 参数（包括-k 开关），后跟一个组名称。 例如，它可能类似于：

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

    请记住此路径和组名称;它们在步骤5和6中使用。

2.  找到以下注册表项：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost 
    ```

    使用唯一名称创建一个新的 REG \_ 多 \_ SZ 值 (例如 **TempGrp**) 。

3.  将此新值设置为要隔离的服务的名称。 不要包括任何目录路径或文件扩展名。 例如，可以将新值 **TempGrp** 设置为等于 **MyService**。

4.  在相同的注册表项下，使用在步骤2中使用的同一名称创建新密钥。 例如：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    现在，SvcHost 密钥包含具有新名称的值，并且还有一个同名的从属密钥。

5.  查找与在步骤1中找到的组名称相同的另一个密钥。 如果有这样的密钥，请检查其中的所有值，并在步骤4中创建的新密钥中创建它们的重复项。

    例如，旧密钥可能命名为：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\LocalServiceNoNetwork 
    ```

    并且它可能包含 **CoInitializeSecurityParam**、 **AuthenticationCapabilities** 和其他值等值。 你将跳到新创建的密钥：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    并在其名称、类型和数据中创建与旧密钥中相同的值。

    如果旧密钥不存在，则无需创建新密钥。

6.  使用以下服务配置工具命令来修改在步骤1中找到的路径：

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    在此命令中， *ServiceName* 是服务的名称， *RevisedPath* 是你为二进制路径名称提供的新值 \_ \_ 。 对于 *RevisedPath*，使用与步骤1中显示的路径完全相同的路径，包括该行上显示的所有选项，只进行一项更改：将-k 开关后面的参数替换为你在步骤2中创建的新注册表值的名称。 将 *RevisedPath* 用引号引起来。 需要等号后的空格。

    例如，命令可能如下所示：

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost.exe -k TempGrp" 
    ```

    你可能希望再次使用 **sc qc** 命令来查看所做的更改。

这些设置将在下一次启动服务时生效。 若要清除旧服务的影响，我们建议你重新启动 Windows，而不是只重启服务。

完成调试后，如果想要将此服务返回给共享服务主机，请再次使用 **sc config** 命令将二进制文件返回到其原始值，并删除已创建的新注册表项和值。

**替代方法：更改服务类型**

1.  发出以下服务配置工具 ( # A0) 命令，其中 *ServiceName* 是服务的名称：

    ```console
    sc config ServiceName type= own 
    ```

    需要等号后的空格。

2.  使用以下命令重新启动服务：
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

不推荐使用此方法，因为它可以改变服务的行为。 如果使用此方法，请使用以下命令在完成调试后恢复为正常行为：

```console
sc config ServiceName type= share 
```

**替代方法：复制 SvcHost 二进制文件**

1.  Svchost.exe 可执行文件位于 Windows 的 system32 目录中。 复制此文件，将其命名为 svhost2.exe，并将其放在 system32 目录中。

2.  发出以下服务配置工具 ( # A0) 命令，其中 *ServiceName* 是服务的名称：

    ```console
    sc qc ServiceName 
    ```

    此命令显示服务的当前配置值。 相关值是二进制 \_ 路径名 \_ ，它指定用于启动服务控制程序的命令行。 在此方案中，由于你的服务尚未隔离，因此此命令行将包含目录路径、Svchost.exe，并且可能会包含一些 SvcHost 参数。 例如，它可能类似于：

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

3.  若要修订此路径，请发出以下命令：

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    在此命令中， *ServiceName* 是服务的名称， *RevisedPath* 是你为二进制路径名称提供的新值 \_ \_ 。 对于 *RevisedPath*，使用与步骤2中显示的路径完全相同的路径，包括该行上显示的所有选项，只进行一项更改：将 Svchost.exe 替换为 Svchost2.exe。 将 *RevisedPath* 用引号引起来。 需要等号后的空格。

    例如，命令可能如下所示：

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost2.exe -k LocalServiceNoNetwork" 
    ```

    可以再次使用 **sc qc** 命令来查看所做的更改。

4.  使用以下命令重新启动服务：
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

不推荐使用此方法，因为它可以改变服务的行为。 如果使用此方法，请在完成调试后使用 **sc config** 命令将路径更改回其原始值。

 

 





