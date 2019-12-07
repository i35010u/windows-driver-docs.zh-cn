---
title: 使用 WinDbg 调试 UWP 应用
description: 可以使用 WinDbg 调试通用 Windows 平台（UWP）应用。
ms.assetid: 1CE337AC-54C0-4EF5-A374-3ECF1D72BA60
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e38cf99e7c9a7159b6cb82b225468fad776c4ece
ms.sourcegitcommit: 9ebed9a7909b0e39a0efb1c23a5435bf36688d05
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74898498"
---
# <a name="debugging-a-uwp-app-using-windbg"></a>使用 WinDbg 调试 UWP 应用


可以使用 WinDbg 调试通用 Windows 平台（UWP）应用。 此方法通常用于高级方案，在这种情况下，不能使用内置 Visual Studio 调试器来完成调试任务。 有关在 Visual Studio 中进行调试的详细信息，请参阅[在 Visual studio 中进行调试](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio?view=vs-2015)。

## <a name="span-idattaching_to_a_uwp_appspanspan-idattaching_to_a_uwp_appspanspan-idattaching_to_a_uwp_appspanattaching-to-a-uwp-app"></a><span id="Attaching_to_a_UWP_app"></span><span id="attaching_to_a_uwp_app"></span><span id="ATTACHING_TO_A_UWP_APP"></span>附加到 UWP 应用


附加到 UWP 进程与附加到用户模式进程相同。 例如，在 WinDbg 中，可以通过**从 "文件" 菜单中选择 "附加到进程"** 或按 F6，附加到正在运行的进程。 有关详细信息，请参阅[使用 WinDbg 调试用户模式进程](debugging-a-user-mode-process-using-windbg.md)。

UWP 应用将不会以它在不进行调试时的相同方式挂起。 若要显式暂停/恢复 UWP 应用，可以使用. suspendpackage 和. resumepackage 命令（详细信息如下）。 有关 UWP 应用使用的流程生命周期管理（PLM）的常规信息，请参阅[应用生命周期](https://docs.microsoft.com/windows/uwp/launch-resume/app-lifecycle)和[启动、恢复以及后台任务](https://docs.microsoft.com/windows/uwp/launch-resume/index)。

## <a name="span-idlaunching_and_debugging__a_uwp_appspanspan-idlaunching_and_debugging__a_uwp_appspanspan-idlaunching_and_debugging__a_uwp_appspanlaunching-and-debugging-a-uwp-app"></a><span id="Launching_and_debugging__a_UWP_app"></span><span id="launching_and_debugging__a_uwp_app"></span><span id="LAUNCHING_AND_DEBUGGING__A_UWP_APP"></span>启动和调试 UWP 应用


-PlmPackage 和-plmApp 命令行参数指示调试器在调试器下启动应用程序。

```console
windbg.exe -plmPackage <PLMPackageName> -plmApp <ApplicationId> [<parameters>]
```

由于多个应用可以包含在一个包中，因此 &lt;PLMPackage&gt; 和 &lt;ApplicationId&gt; 参数都是必需的。 这是参数的汇总。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>参数</strong></td>
<td align="left"><strong>描述</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left">应用程序包的名称。 使用 querypackages 命令可列出所有 UWP 应用程序。 不要提供包位置的路径，只提供包名称。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>ApplicationId 位于应用程序清单文件中，可使用本主题中讨论的 querypackage 或 querypackages 命令查看。</p>
<p>有关应用程序清单文件的详细信息，请参阅<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">应用包清单</a>。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;参数&gt;]</td>
<td align="left"><p>传递给应用的可选参数。 并非所有应用都使用或要求参数。</p></td>
</tr>
</tbody>
</table>

 

**HelloWorld 示例**

为了演示 UWP 调试，本主题使用[创建 "Hello，world" 应用（XAML）](https://docs.microsoft.com/windows/uwp/get-started/create-a-hello-world-app-xaml-universal)中所述的 HelloWorld 示例。

若要创建可行的测试应用，只需完成实验室的第三步。

**查找完整的包名称和 AppId**

使用 querypackages 命令可找到完整的包名称和 AppId。 键入 querypackages，然后按 user CRTL + F 在应用程序名称的输出中向上搜索，例如 HelloWorld。 使用 CTRL + F 定位项时，它会显示包的完整名称，例如*e24caf14-8483-4743-b80c-ca46c28c75df\_1.0.0.0\_x86\_\_97ghe447vaan8*和*应用程序*的 AppId。

示例：

```dbgcmd
0:000>  .querypackages 
...
Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Unknown
AppId: App
...
```

**查看清单中的基本包名称**

若要进行故障排除，你可能想要在 Visual Studio 中查看基本包名称。

若要在 Visual Studio 中查找基包名称，请单击 "项目资源管理器" 中的 Applicationmanifest.xml 文件。 基本包名称将显示在 "打包" 选项卡的 "包名称" 下。 默认情况下，包名称将为 GUID，例如*e24caf14-8483-4743-b80c-ca46c28c75df*。

若要使用记事本查找基包名称，请打开 Applicationmanifest.xml 文件并找到 "**标识名称**" 标记。

```xml
  <Identity
    Name="e24caf14-8483-4743-b80c-ca46c28c75df"
    Publisher="CN= User1"
    Version="1.0.0.0" />
```

**在清单中查找应用程序 Id**

若要在安装的 UWP 应用的清单文件中找到应用程序 Id，请查找*应用程序 id*条目。

例如，对于 hello world 应用程序，应用程序 ID 为*app*。

```xml
<Application Id="App"
      Executable="$targetnametoken$.exe"
      EntryPoint="HelloWorld.App">
```

**WinDbg 命令行示例**

这是一个示例命令行，使用完整的包名称和 AppId 在调试器下加载 HelloWorld 应用。

```console
windbg.exe -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

## <a name="span-idlaunching_a_background_task_under_the_debuggerspanspan-idlaunching_a_background_task_under_the_debuggerspanspan-idlaunching_a_background_task_under_the_debuggerspanlaunching-a-background-task-under-the-debugger"></a><span id="Launching_a_background_task_under_the_debugger"></span><span id="launching_a_background_task_under_the_debugger"></span><span id="LAUNCHING_A_BACKGROUND_TASK_UNDER_THE_DEBUGGER"></span>在调试器下启动后台任务


可以使用 TaskId 从命令行在调试器下显式启动后台任务。 为此，请使用-plmPackage 和-plmBgTaskId 命令行参数：

```console
windbg.exe -plmPackage <PLMPackageName> -plmBgTaskId <BackgroundTaskId>
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>参数</strong></td>
<td align="left"><strong>描述</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left"><p>应用程序包的名称。 使用 querypackages 命令可列出所有 UWP 应用程序。 不要提供包位置的路径，只提供包名称。</p></td>
</tr>
<tr class="odd">
<td align="left">&lt;BackgroundTaskId&gt;</td>
<td align="left"><p>BackgroundTaskId 可以使用 querypackages 命令查找，如下所述。</p>
<p>有关应用程序清单文件的详细信息，请参阅<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">应用包清单</a>。</p></td>
</tr>
</tbody>
</table>

 

这是在调试器下加载 SDKSamples 代码的示例。

```console
windbg.exe -plmPackage Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe -plmBgTaskId {ee4438ee-22db-4cdd-85e4-8ad8a1063523}
```

你可以尝试后台任务示例代码，以熟悉 UWP 调试。 它可以在[后台任务示例](https://go.microsoft.com/fwlink/p/?linkid=2112776)中下载。

使用 querypackages 命令可找到 BackgroundTaskId。 使用 CTRL + F 查找应用程序，然后找到 "*后台任务 Id* " 字段。 若要显示关联的后台任务名称和任务 Id，必须运行后台任务。

```dbgcmd
0:000> .querypackages
...
Package Full Name: Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x86__8wekyb3d8bbwe
Package Display Name: BackgroundTask C++ sample
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
Publisher Display Name: Microsoft Corporation
Install Folder: C:\Users\user1\Documents\Visual Studio 2015\Projects\Background_task_sample\C++\Debug\BackgroundTask.Windows\AppX
Package State: Running
AppId: BackgroundTask.App
Background Task Name: SampleBackgroundTask
Background Task Id: {ee4438ee-22db-4cdd-85e4-8ad8a1063523}
...
```

如果你知道你可以使用的完整包名称，则可以使用 querypackage 来显示 "*后台任务 Id* " 字段。

还可以通过使用 PLMDebug 的 enumerateBgTasks 选项来查找 BackgroundTaskId。 有关 PMLDebug utiltity 的详细信息，请参阅[**PLMDebug**](plmdebug.md)。

```console
C:\Program Files\Debugging Tools for Windows (x64)>PLMDebug /enumerateBgTasks Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe
Package full name is Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe.
Background Tasks:
SampleBackgroundTask : {C05806B1-9647-4765-9A0F-97182CEA5AAD}

SUCCEEDED
```

## <a name="span-iddebugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_spanspan-iddebugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_spanspan-iddebugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_spandebugging-a-uwp-process-remotely-using-a-process-server-dbgsrv"></a><span id="Debugging_a_UWP_process_remotely_using_a_Process_Server__DbgSrv_"></span><span id="debugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_"></span><span id="DEBUGGING_A_UWP_PROCESS_REMOTELY_USING_A_PROCESS_SERVER__DBGSRV_"></span>使用进程服务器远程调试 UWP 进程（DbgSrv）


所有-plm\* 命令都能与 dbgsrv 正常配合使用。 若要使用 dbgsrv 进行调试，请将-premote 开关与 dbgsrv 的连接字符串一起使用：

```console
windbg.exe -premote npipe:pipe=fdsa,server=localhost -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

有关-premote 选项的详细信息，请参阅[进程服务器（用户模式）](process-servers--user-mode-.md)和[进程服务器示例](process-server-examples.md)。

## <a name="span-idsummary_of_uwp_app_commandsspanspan-idsummary_of_uwp_app_commandsspanspan-idsummary_of_uwp_app_commandsspansummary-of-uwp-app-commands"></a><span id="Summary_of_UWP_app_commands"></span><span id="summary_of_uwp_app_commands"></span><span id="SUMMARY_OF_UWP_APP_COMMANDS"></span>UWP 应用命令摘要


本部分提供 UWP 应用调试器命令的摘要

**正在收集包信息**

**.querypackage**

Querypackage 显示 UWP 应用程序的状态。 例如，如果应用程序正在运行，则它可以处于*活动*状态。

```dbgcmd
.querypackage <PLMPackageName>
```

示例：

```dbgcmd
0:000> .querypackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Running
AppId: App
Executable: HelloWorld.exe
```

**.querypackages**

Querypackages 命令将列出所有已安装的 UWP 应用程序及其当前状态。

```dbgcmd
.querypackages
```

示例：

```dbgcmd
0:000> .querypackages
...
Package Full Name: Microsoft.MicrosoftSolitaireCollection_3.9.5250.0_x64__8wekyb3d8bbwe
Package Display Name: Microsoft Solitaire Collection
Version: 3.9.5250.0
Processor Architecture: x64
Publisher: CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
Publisher Display Name: Microsoft Studios
Install Folder: C:\Program Files\WindowsApps\Microsoft.MicrosoftSolitaireCollection_3.9.5250.0_x64__8wekyb3d8bbwe
Package State: Unknown
AppId: App

Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Running
AppId: App
Executable: HelloWorld.exe

Package Full Name: Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x86__8wekyb3d8bbwe
Package Display Name: BackgroundTask C++ sample
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
Publisher Display Name: Microsoft Corporation
Install Folder: C:\Users\user1\Documents\Visual Studio 2015\Projects\Background_task_sample\C++\Debug\BackgroundTask.Windows\AppX
Package State: Unknown
AppId: BackgroundTask.App

...
```

**启动应用程序以进行调试**

**.createpackageapp**

Createpackageapp 命令启用调试并启动 UWP 应用程序。

```dbgcmd
.createpackageapp <PLMPackageName> <ApplicationId> [<parameters>] 
```

下表列出了 createpackageapp 的参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>参数</strong></td>
<td align="left"><strong>描述</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left">应用程序包的名称。 使用 querypackages 命令可列出所有 UWP 应用程序。 不要提供包位置的路径，只提供包名称。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>可以使用 querypackage 或 querypackages 定位 ApplicationId，如本主题前面所述。</p>
<p>有关应用程序清单文件的详细信息，请参阅<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">应用包清单</a>。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;参数&gt;]</td>
<td align="left">传递给应用程序的可选参数。 并非所有应用程序都需要或使用这些可选参数。</td>
</tr>
</tbody>
</table>

 

示例：

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

**启用和禁用调试命令的使用**

**.enablepackagedebug**

Enablepackagedebug 命令启用 UWP 应用程序调试。 在调用任何挂起、继续或终止函数之前，必须使用 enablepackagedebug。

请注意，createpackageapp 命令还支持调试应用程序。

```dbgcmd
.enablepackagedebug <PLMPackageName>
```

示例：

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.disablepackagedebug**

Disablepackagedebug 命令禁用 UWP 应用程序调试。

```dbgcmd
.disablepackagedebug <PLMPackageName>
```

示例：

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**启动和停止应用程序**

请注意，"挂起"、"恢复" 和 "终止" 会影响包中当前正在运行的所有应用。

**.suspendpackage**

Suspendpackage 命令挂起 UWP 应用程序。

```dbgcmd
.suspendpackage <PLMPackageName> 
```

示例：

```dbgcmd
0:024> .suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.resumepackage**

Resumepackage 命令恢复 UWP 应用程序。

```dbgcmd
.resumepackage <PLMPackageName> 
```

示例：

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.terminatepackageapp**

Terminatepackageapp 命令终止包中的所有 UWP 应用程序。

```dbgcmd
.terminatepackageapp <PLMPackageName> 
```

示例：

```dbgcmd
.terminatepackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**后台任务**

**.activatepackagebgtask**

Activatepackagebgtask 命令启用调试，并启动 UWP 后台任务。

```dbgcmd
 .activatepackagebgtask <PLMPackageName> <bgTaskId>
```

示例：

```dbgcmd
.activatepackagebgtask Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe {C05806B1-9647-4765-9A0F-97182CEA5AAD}
```

## <a name="span-idusage_examplesspanspan-idusage_examplesspanspan-idusage_examplesspanusage-examples"></a><span id="Usage_Examples"></span><span id="usage_examples"></span><span id="USAGE_EXAMPLES"></span>用法示例


**在应用程序启动时附加调试器**

假设你有一个名为 HelloWorld 的应用程序，该应用程序位于名为 e24caf14-8483-4743-b80c-ca46c28c75df\_1.0.0.0\_x86\_\_97ghe447vaan8。 通过显示所有已安装的包的完整名称和运行状态，验证是否已安装包。 在命令提示符窗口中，输入以下命令。 可以使用 CTRL + F 在命令输出中搜索 HelloWorld 的应用名称。

```dbgcmd
.querypackages 
...

Package Full Name: e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
Package Display Name: HelloWorld
Version: 1.0.0.0
Processor Architecture: x86
Publisher: CN=user1
Publisher Display Name: user1
Install Folder: c:\users\user1\documents\visual studio 2015\Projects\HelloWorld\HelloWorld\bin\x86\Release\AppX
Package State: Unknown
AppId: App

...
```

使用 createpackageapp 启动并附加到应用程序。 Createpackageapp 命令还启用对应用程序的调试。

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

完成调试后，请使用 disablepackagedebug 命令递减包的调试引用计数。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**将调试程序附加到已在运行的应用程序**

假设要将 WinDbg 附加到已在运行的 MyApp。 在 WinDbg 的 "**文件**" 菜单上，选择 "**附加到进程**"。 记下 MyApp 的进程 ID。 假设进程 ID 为4816。 为包含 MyApp 的包增加调试引用计数。

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

在 WinDbg 的 "**附加到进程**" 对话框中，选择 "处理 4816"，然后单击 "确定"。 WinDbg 将附加到 MyApp。

完成调试后，请使用 disablepackagedebug 命令递减包的调试引用计数。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**手动暂停和恢复应用**

请按照以下步骤手动暂停和恢复应用。 首先，请为包含应用的包增加调试引用计数。

```dbgcmd
.enablepackagedebug  e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

暂停包。 将调用应用的挂起处理程序，这对于调试很有帮助。

```dbgcmd
.suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

完成调试后，继续执行包。

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

最后，减小包的调试引用计数。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 WinDbg 进行调试](debugging-using-windbg.md)

 

 






