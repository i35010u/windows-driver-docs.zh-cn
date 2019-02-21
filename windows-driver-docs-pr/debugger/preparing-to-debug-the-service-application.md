---
title: 调试服务应用程序的准备工作
description: 调试服务应用程序的准备工作
ms.assetid: 332b7bcf-22e4-4b98-bcb3-3646f8bd63fd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2967f4b5d31b49adbfbf25f9f967948ffb761429
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525419"
---
# <a name="preparing-to-debug-the-service-application"></a>调试服务应用程序的准备工作


本主题列出了所有可能无需在调试服务应用程序之前的预备步骤。 你的方案中需要哪些步骤取决于其附加已选择，但选择的调试配置的选项。 有关这些选项的列表，请参阅[选择最佳方法](choosing-the-best-method.md)。

本主题中所述的预备步骤的每个指定在其下的所需的条件。 可以按任意顺序完成这些步骤。

### <a name="span-idenabling-the-debugging-of-the-initializationcodespanspan-idenablingthedebuggingoftheinitializationcodespan-enabling-the-debugging-of-the-initialization-code"></a><span id="enabling-the-debugging-of-the-initialization_code"></span><span id="ENABLING_THE_DEBUGGING_OF_THE_INITIALIZATION_CODE"></span> 启用调试初始化代码

如果你打算调试服务应用程序从一开始其执行，包括其初始化代码，则需要此预备步骤。

找到或创建以下注册表项，其中*ProgramName*是服务应用程序的可执行文件的名称：

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\ProgramName 
```

*ProgramName*应包括文件扩展名，而不是路径。 例如， *ProgramName*可能 Myservice.exe 或 Thisservice.dll。

在此注册表项下创建名为一个字符串数据值**调试器**。 此字符串的值应设置为调试程序的完整路径和文件名称附加到服务应用程序。

-   如果你打算在本地进行调试，使用如下所示的字符串：

    ```console
    c:\Debuggers\windbg.exe 
    ```

    如果在运行 Windows Vista 或更高版本的 Windows，则不选择此选项。

-   如果您计划使用远程调试，请使用-noio 选项指定 NTSD。 这将导致 NTSD 来运行时没有任何控制台中的其自己，只能通过远程连接。 例如：

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -noio -y SymbolPath 
    ```

    如果在调试会话开始 Windows 完全加载之前，你可能无法从远程共享; 访问符号在这种情况下，必须使用本地符号。 *服务器传送*必须指定实现由 Windows 内核，而无需与用户模式服务，例如 TCP 或 NPIPE 进行连接的传输协议。 有关的语法*服务器传送*，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。

-   如果您计划以控制用户模式下的调试程序与内核模式调试程序，请使用-d 选项指定 NTSD。 例如：

    ```console
    c:\Debuggers\ntsd.exe -d -y SymbolPath 
    ```

    如果你打算使用此方法和用户模式符号从符号服务器访问，应与远程调试合并此方法。 在这种情况下，使用-ddefer 选项来指定 NTSD。 选择实现由 Windows 内核，而无需与用户模式服务，例如 TCP 或 NPIPE 进行连接的传输协议。 例如：

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -ddefer -y SymbolPath 
    ```

    有关详细信息，请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

完成编辑该注册表后，每当启动或重新启动具有此名称的服务时启动调试器。

### <a name="span-idenabling-the-service-application-to-break-into-the-debuggerspanspan-idenablingtheserviceapplicationtobreakintothedebuggerspan-enabling-the-service-application-to-break-into-the-debugger"></a><span id="enabling-the-service-application-to-break-into-the-debugger"></span><span id="ENABLING_THE_SERVICE_APPLICATION_TO_BREAK_INTO_THE_DEBUGGER"></span> 启用服务应用程序运行中断到调试器

如果你想要在发生故障或遇到的异常时中断调试器服务应用程序，，则需要此预备步骤。 如果你想要中断调试器通过调用服务应用程序，此步骤也是必需**DebugBreak**函数。

**请注意**  已启用调试的初始化代码 （"启用调试的初始化代码"的子部分中所述的步骤），如果应跳过此步骤。 启用调试初始化代码后，在启动时，它会导致所有崩溃、 异常，并调用，调试器将附加到服务应用程序**DebugBreak**要路由到调试程序而无需其他所需的准备工作。

 

此预备步骤涉及在事后调试器注册所选的调试器。 这是通过使用调试器命令行上的-iae 或-iaec 选项。 我们建议为以下命令，但如果你想要改变它们，请参阅中的语法详细信息[启用事后调试](enabling-postmortem-debugging.md)。

-   如果你打算在本地进行调试，请使用如下所示的命令：

    ```console
    windbg -iae 
    ```

    如果在运行 Windows Vista 或更高版本的 Windows，则不选择此选项。

-   如果您计划使用远程调试，请使用-noio 选项指定 NTSD。 这将导致 NTSD 来运行时没有任何控制台中的其自己，只能通过远程连接。 若要安装包括事后调试器-server 参数，则必须手动编辑注册表;有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。 例如，**调试器**的值**AeDebug**密钥可能如下所示：

    ```console
    ntsd -server npipe:pipe=myproc%x -noio -p %ld -e %ld -g -y SymbolPath 
    ```

    在管道规范中， **%x**令牌将被替换为启动该调试器的进程的进程 ID。 这可保证，如果多个进程启动事后调试程序，每个都有唯一的管道名称。 如果在调试会话开始 Windows 完全加载之前，你可能无法从远程共享; 访问符号在这种情况下，必须使用本地符号。 *服务器传送*必须指定实现由 Windows 内核，而无需与用户模式服务，例如 TCP 或 NPIPE 进行连接的传输协议。 有关的语法*服务器传送*，请参阅[**激活调试服务器**](activating-a-debugging-server.md)。

-   如果您计划以控制用户模式下的调试程序与内核模式调试程序，请使用-d 选项指定 NTSD。 例如：

    ```console
    ntsd -iaec -d -y SymbolPath 
    ```

    如果您选择此方法，并且想要访问用户模式符号从符号服务器，应将此方法合并与远程调试。 在这种情况下，使用-ddefer 选项来指定 NTSD。 选择实现由 Windows 内核，而无需与用户模式服务，例如 TCP 或 NPIPE 进行连接的传输协议。 若要安装包括事后调试器-server 参数，则必须手动编辑注册表;有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。 例如，**调试器**的值**AeDebug**密钥可能如下所示：

    ```console
    ntsd -server npipe:pipe=myproc%x -ddefer -p %ld -e %ld -g -y SymbolPath 
    ```

    有关详细信息，请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

发出以下命令之一，事后调试器处于已注册。 将启动此调试器，包括服务应用程序，任何用户模式程序遇到的异常或运行时**DebugBreak**函数。

### <a name="span-idadjusting-the-service-application-timeoutspanspan-idadjustingtheserviceapplicationtimeoutspan-adjusting-the-service-application-timeout"></a><span id="adjusting-the-service-application-timeout"></span><span id="ADJUSTING_THE_SERVICE_APPLICATION_TIMEOUT"></span> 调整服务应用程序超时

如果您计划自动启动调试器 （当服务启动时或当遇到异常），则需要此预备步骤。

找到以下注册表项：

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control
```

此项下找到或创建名为的 DWORD 数据值**ServicesPipeTimeout**。 将此条目设置为以毫秒为单位的所需服务超时前等待的时间量。例如，值为 60000 是一分钟，而 86400000 的值为 24 小时。 如果未设置此注册表值，默认超时为大约 30 秒。

此值的重要性是时钟开始运行并启动每个服务时，达到超时值时，终止任何调试器附加到该服务。 因此，您选择的值应超过的服务和在调试会话完成启动之间经过的时间总量。

此设置适用于每个服务都启动或重新启动完成编辑注册表后。 如果某些服务崩溃或挂起和此设置是仍然有效时，该问题未检测到 Windows。 因此，您应仅当正在调试时，才使用此设置，并返回到其原始值的注册表项，在调试完成后。

### <a name="span-idisolating-the-servicespanspan-idisolatingtheservicespan-isolating-the-service"></a><span id="isolating-the-service"></span><span id="ISOLATING_THE_SERVICE"></span> 隔离服务

有时，在单一服务主机 (Svchost) 进程中组合多个服务。 如果你想要调试此类服务，必须首先将其隔离到单独的 Svchost 进程中。

有三种方法可以依据隔离服务。 Microsoft 建议移动到其自己组方法，按如下所示的服务。 （更改服务类型和复制 SvcHost 二进制文件） 的替代方法可用于临时调试，但因为它们会更改该服务的运行的方式，它们不是第一种方法不如可靠。

**首选的方法：将服务移到其自己的组**

1.  发出以下服务配置工具 (Sc.exe) 命令，其中*ServiceName*是服务名称：

    ```console
    sc qc ServiceName 
    ```

    这将显示该服务的当前配置值。 感兴趣的值是二元\_路径\_NAME，该值指定用来启动服务管理程序的命令行。 在此方案中，因为你的服务还不是隔离的此命令行中将包括目录路径、 Svchost.exe 和一些 SvcHost 参数，包括-k 开关，然后按组名称。 例如，它可能如下所示：

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

    请记住此路径和组名称;步骤 5 和 6 中使用它们。

2.  找到以下注册表项：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost 
    ```

    创建新的 REG\_多\_SZ 值，该值具有一个唯一的名称 (例如， **TempGrp**)。

3.  将此新值设置为你想要隔离服务的名称。 不包括任何目录路径或文件扩展名。 例如，你可能会设置新值**TempGrp**等于**MyService**。

4.  在相同的注册表项下与步骤 2 中使用的相同名称创建新的密钥。 例如：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    现在 SvcHost 密钥包含具有新名称的值，并还都有一个从属键与此相同的名称。

5.  查找与在步骤 1 中找到的组同名的 SvcHost 密钥从属于另一个键。 如果此类密钥存在，检查所有的值，并在步骤 4 中创建的新项中创建这些重复项。

    例如，旧密钥可能会被命名为此：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\LocalServiceNoNetwork 
    ```

    并且它可能包含值，如**CoInitializeSecurityParam**， **AuthenticationCapabilities**，和其他值。 你将转到新创建的密钥：

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    并在其中都相同的名称、 类型和数据中的旧密钥创建值。

    旧密钥不存在，如果您不需要创建新的密钥。

6.  使用以下服务配置工具命令来修改在步骤 1 中找到的路径：

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    在此命令中， *ServiceName*是服务的名称，并*RevisedPath*是你所提供的二进制文件的新值\_路径\_名称。 有关*RevisedPath*，使用完全相同的路径的与显示在步骤 1，包含使只有一个更改的行上显示的所有选项： 替换为以下-k 参数切换使用新的注册表值的名称步骤 2 中创建。 将括*RevisedPath*引号引起来。 等号后面的空格是必需的。

    例如，您的命令可能如下所示：

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost.exe -k TempGrp" 
    ```

    您可能想要使用**sc qc**命令再次以查看所做的更改。

这些设置将在的下次启动该服务时生效。 若要清除旧的服务的影响，我们建议您重新启动 Windows 而不是只需重新启动服务。

已完成调试过程中，如果你想要返回到共享的服务主机，使用此服务后**sc config**命令再次返回到其原始值的二进制文件的路径，并删除新的注册表密钥和值创建...

**另一种方法：更改服务类型**

1.  发出以下服务配置工具 (Sc.exe) 命令，其中*ServiceName*是服务名称：

    ```console
    sc config ServiceName type= own 
    ```

    等号后面的空格是必需的。

2.  使用以下命令重新启动该服务：
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

此替代方法不是建议的方法，因为它可以更改服务的行为。 如果您使用此方法，使用以下命令以在调试完成后恢复为正常行为：

```console
sc config ServiceName type= share 
```

**另一种方法：复制 SvcHost 二进制文件**

1.  Svchost.exe 可执行文件位于 Windows system32 目录中。 使此文件的副本、 其命名为 svhost2.exe，并将其放在 system32 目录中。

2.  发出以下服务配置工具 (Sc.exe) 命令，其中*ServiceName*是服务名称：

    ```console
    sc qc ServiceName 
    ```

    此命令显示服务的当前配置值。 感兴趣的值是二元\_路径\_NAME，该值指定用来启动服务管理程序的命令行。 在此方案中，因为你的服务还不是隔离的此命令行中将包括目录路径、 Svchost.exe 和可能某些 SvcHost 参数。 例如，它可能如下所示：

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

3.  若要修改此路径，请发出以下命令：

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    在此命令中， *ServiceName*是服务的名称，并*RevisedPath*是你所提供的二进制文件的新值\_路径\_名称。 有关*RevisedPath*，使用完全相同的路径的与显示在步骤 2，其中包括使只有一个更改的行中所显示的所有选项： Svchost.exe 替换 Svchost2.exe。 将括*RevisedPath*引号引起来。 等号后面的空格是必需的。

    例如，您的命令可能如下所示：

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost2.exe -k LocalServiceNoNetwork" 
    ```

    可以使用**sc qc**命令再次以查看所做的更改。

4.  使用以下命令重新启动服务：
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

此替代方法不是建议的方法，因为它可以更改服务的行为。 如果您使用此方法，使用**sc config**命令以在调试完成后恢复为其原始值更改的路径。

 

 





