---
title: 使用 WinDbg 调试 UWP 应用
description: 您可以调试使用 WinDbg 的通用 Windows 平台 (UWP) 应用。
ms.assetid: 1CE337AC-54C0-4EF5-A374-3ECF1D72BA60
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5756bb217cef8a051426f6bbaa704d65d916ca38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366939"
---
# <a name="debugging-a-uwp-app-using-windbg"></a>使用 WinDbg 调试 UWP 应用


您可以调试使用 WinDbg 的通用 Windows 平台 (UWP) 应用。 此方法将通常用于高级方案，其中不能完成 Visual Studio 调试器中使用内置的调试任务。 有关在 Visual Studio 中调试的详细信息，请参阅[Visual Studio 中调试](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio?view=vs-2015)。

## <a name="span-idattachingtoauwpappspanspan-idattachingtoauwpappspanspan-idattachingtoauwpappspanattaching-to-a-uwp-app"></a><span id="Attaching_to_a_UWP_app"></span><span id="attaching_to_a_uwp_app"></span><span id="ATTACHING_TO_A_UWP_APP"></span>将连接到 UWP 应用


附加到 UWP 进程是与附加到用户模式进程相同的。 例如，在 WinDbg 中您可以将附加到正在运行的进程通过选择**从文件附加到进程**菜单或通过按 F6。 有关详细信息，请参阅[调试用户模式进程使用 WinDbg](debugging-a-user-mode-process-using-windbg.md)。

UWP 应用不将其挂起的不调试时的表现的方式。 若要显式挂起/继续 UWP 应用，可以使用.suspendpackage 和.resumepackage 命令 （下面的详细信息）。 在进程生命周期管理 (PLM) 使用的 UWP 应用的一般信息，请参阅[应用程序生命周期](https://docs.microsoft.com/windows/uwp/launch-resume/app-lifecycle)并[Launching，resuming，和后台任务](https://docs.microsoft.com/windows/uwp/launch-resume/index)。

## <a name="span-idlaunchinganddebuggingauwpappspanspan-idlaunchinganddebuggingauwpappspanspan-idlaunchinganddebuggingauwpappspanlaunching-and-debugging-a-uwp-app"></a><span id="Launching_and_debugging__a_UWP_app"></span><span id="launching_and_debugging__a_uwp_app"></span><span id="LAUNCHING_AND_DEBUGGING__A_UWP_APP"></span>启动并调试 UWP 应用


-PlmPackage 和-plmApp 命令行参数指示调试程序启动应用程序在调试器下。

```console
windbg.exe -plmPackage <PLMPackageName> -plmApp <ApplicationId> [<parameters>]
```

由于多个应用程序可以包含在单个包中，同时&lt;PLMPackage&gt;并&lt;ApplicationId&gt;参数是必需的。 这是参数的摘要。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>参数</strong></td>
<td align="left"><strong>说明</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left">应用程序包的名称。 使用.querypackages 命令以列出所有 UWP 应用程序。 不要提供包的位置的路径，提供只是包的名称。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>ApplicationId 位于应用程序清单文件中，可以使用本主题中所述.querypackage 或.querypackages 命令来查看。</p>
<p>有关应用程序清单文件的详细信息，请参阅<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">应用程序包清单</a>。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;parameters&gt;]</td>
<td align="left"><p>可选参数传递到应用。 并非所有应用程序使用或不需要参数。</p></td>
</tr>
</tbody>
</table>

 

**HelloWorld 示例**

为了演示 UWP 调试，本主题使用 HelloWorld 示例中所述[创建"Hello，world"应用 (XAML)](https://docs.microsoft.com/windows/uwp/get-started/create-a-hello-world-app-xaml-universal)。

若要创建一个可正常工作的测试应用，它只是用来完成到实验室的第三步。

**查找完整包名称和 AppId**

使用.querypackages 命令查找完整包名称和 AppId。 键入.querypackages，然后选择用户 CRTL + F 将该应用程序名称，例如 HelloWorld 的输出中向上搜索。 使用 CTRL + F 定位该条目时，它会显示包完整名称，例如*e24caf14-8483-4743-b80c-ca46c28c75df\_1.0.0.0\_x86\_\_97ghe447vaan8*和AppId*应用*。

例如：

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

**查看中的基础包名称在清单中**

有关故障排除，您可能想要在 Visual Studio 中查看基础包名称。

若要在 Visual Studio 中找到基程序包名称，单击项目资源管理器中的 ApplicationManifest.xml 文件。 基础包名称将显示在打包选项卡下，为"包名称"。 默认情况下，包名称将是一个 GUID，例如*e24caf14-8483-4743-b80c-ca46c28c75df*。

若要使用记事本中找到的基本包名称，打开 ApplicationManifest.xml 文件并找到**标识名称**标记。

```xml
  <Identity
    Name="e24caf14-8483-4743-b80c-ca46c28c75df"
    Publisher="CN= User1"
    Version="1.0.0.0" />
```

**在清单中查找应用程序 Id**

若要在已安装的 UWP 应用的清单文件中查找应用程序 Id，寻找*应用程序 Id*条目。

例如，对于你好 world 应用应用程序 ID 是*应用*。

```xml
<Application Id="App"
      Executable="$targetnametoken$.exe"
      EntryPoint="HelloWorld.App">
```

**WinDbg 命令行示例**

这是加载待使用的完整包名称和 AppId 在调试器的 HelloWorld 应用程序的示例命令行。

```console
windbg.exe -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

## <a name="span-idlaunchingabackgroundtaskunderthedebuggerspanspan-idlaunchingabackgroundtaskunderthedebuggerspanspan-idlaunchingabackgroundtaskunderthedebuggerspanlaunching-a-background-task-under-the-debugger"></a><span id="Launching_a_background_task_under_the_debugger"></span><span id="launching_a_background_task_under_the_debugger"></span><span id="LAUNCHING_A_BACKGROUND_TASK_UNDER_THE_DEBUGGER"></span>启动在调试器下的后台任务


可以从命令行使用 TaskId 在调试器下显式启动后台任务。 若要执行此操作，请使用-plmPackage 和-plmBgTaskId 命令行参数：

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
<td align="left"><strong>说明</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left"><p>应用程序包的名称。 使用.querypackages 命令以列出所有 UWP 应用程序。 不要提供包的位置的路径，提供只是包的名称。</p></td>
</tr>
<tr class="odd">
<td align="left">&lt;BackgroundTaskId&gt;</td>
<td align="left"><p>BackgroundTaskId 可位于使用.querypackages 命令如下所述。</p>
<p>有关应用程序清单文件的详细信息，请参阅<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">应用程序包清单</a>。</p></td>
</tr>
</tbody>
</table>

 

这是加载在调试器下的 SDKSamples.BackgroundTask 代码的示例。

```console
windbg.exe -plmPackage Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe -plmBgTaskId {ee4438ee-22db-4cdd-85e4-8ad8a1063523}
```

您可以尝试以熟悉 UWP 调试的后台任务示例代码。 可以在下载[后台任务示例](https://code.msdn.microsoft.com/windowsapps/Background-Task-Sample-9209ade9)。

使用.querypackages 命令来查找 BackgroundTaskId。 使用 CTRL-F 以找到应用，然后找到*后台任务 Id*字段。 必须运行后台任务以显示相关联的后台任务名称和任务 id。

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

如果您知道完整的程序包名称可以使用.querypackage 以显示*后台任务 Id*字段。

你还可以通过使用 PLMDebug enumerateBgTasks 选项找到 BackgroundTaskId。 有关 PMLDebug 实用程序的详细信息，请参阅[ **PLMDebug**](plmdebug.md)。

```console
C:\Program Files\Debugging Tools for Windows (x64)>PLMDebug /enumerateBgTasks Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe
Package full name is Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe.
Background Tasks:
SampleBackgroundTask : {C05806B1-9647-4765-9A0F-97182CEA5AAD}

SUCCEEDED
```

## <a name="span-iddebuggingauwpprocessremotelyusingaprocessserverdbgsrvspanspan-iddebuggingauwpprocessremotelyusingaprocessserverdbgsrvspanspan-iddebuggingauwpprocessremotelyusingaprocessserverdbgsrvspandebugging-a-uwp-process-remotely-using-a-process-server-dbgsrv"></a><span id="Debugging_a_UWP_process_remotely_using_a_Process_Server__DbgSrv_"></span><span id="debugging_a_uwp_process_remotely_using_a_process_server__dbgsrv_"></span><span id="DEBUGGING_A_UWP_PROCESS_REMOTELY_USING_A_PROCESS_SERVER__DBGSRV_"></span>调试远程使用进程服务器 (DbgSrv) 的 UWP 进程


所有-plm\*命令与 dbgsrv 正常工作。 若要使用 dbgsrv 进行调试，请使用-premote 开关 dbgsrv 的连接字符串：

```console
windbg.exe -premote npipe:pipe=fdsa,server=localhost -plmPackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 -plmApp App
```

有关详细信息-premote 选项，请参阅[的进程服务器 （用户模式）](process-servers--user-mode-.md)并[进程服务器示例](process-server-examples.md)。

## <a name="span-idsummaryofuwpappcommandsspanspan-idsummaryofuwpappcommandsspanspan-idsummaryofuwpappcommandsspansummary-of-uwp-app-commands"></a><span id="Summary_of_UWP_app_commands"></span><span id="summary_of_uwp_app_commands"></span><span id="SUMMARY_OF_UWP_APP_COMMANDS"></span>UWP 应用命令摘要


本部分提供 UWP 应用的调试器命令的摘要

**正在收集包信息**

**.querypackage**

.Querypackage 显示 UWP 应用程序的状态。 例如，如果应用正在运行，它可以是在*Active*状态。

```dbgcmd
.querypackage <PLMPackageName>
```

例如：

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

.Querypackages 命令列出所有已安装的 UWP 应用程序及其当前状态。

```dbgcmd
.querypackages
```

例如：

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

**启动 app 进行调试。**

**.createpackageapp**

.Createpackageapp 命令启用调试，并启动 UWP 应用程序。

```dbgcmd
.createpackageapp <PLMPackageName> <ApplicationId> [<parameters>] 
```

此表列出了.createpackageapp 的参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><strong>参数</strong></td>
<td align="left"><strong>说明</strong></td>
</tr>
<tr class="even">
<td align="left">&lt;PLMPackageName&gt;</td>
<td align="left">应用程序包的名称。 使用.querypackages 命令以列出所有 UWP 应用程序。 不要提供包的位置的路径，提供只是包的名称。</td>
</tr>
<tr class="odd">
<td align="left">&lt;ApplicationId&gt;</td>
<td align="left"><p>ApplicationId 可位于使用.querypackage 或.querypackages，如本主题中前面所述。</p>
<p>有关应用程序清单文件的详细信息，请参阅<a href="https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest" data-raw-source="[App package manifest](https://docs.microsoft.com/uwp/schemas/appxpackage/appx-package-manifest)">应用程序包清单</a>。</p></td>
</tr>
<tr class="even">
<td align="left">[&lt;parameters&gt;]</td>
<td align="left">传递给应用程序的可选参数。 并非所有应用程序需要或不使用这些可选参数。</td>
</tr>
</tbody>
</table>

 

例如：

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

**启用和禁用使用调试命令**

**.enablepackagedebug**

.Enablepackagedebug 命令为启用调试 UWP 应用程序。 必须使用.enablepackagedebug 在挂起的任何调用之前，恢复或终止函数。

请注意.createpackageapp 命令还启用应用程序的调试。

```dbgcmd
.enablepackagedebug <PLMPackageName>
```

例如：

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.disablepackagedebug**

.Disablepackagedebug 命令禁用调试 UWP 应用程序。

```dbgcmd
.disablepackagedebug <PLMPackageName>
```

例如：

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**启动和停止应用程序**

请注意，挂起、 继续和终止所有当前包中运行应用程序的影响。

**.suspendpackage**

.Suspendpackage 命令，挂起的 UWP 应用程序。

```dbgcmd
.suspendpackage <PLMPackageName> 
```

例如：

```dbgcmd
0:024> .suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.resumepackage**

.Resumepackage 命令恢复一个 UWP 应用程序。

```dbgcmd
.resumepackage <PLMPackageName> 
```

例如：

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**.terminatepackageapp**

.Terminatepackageapp 命令终止所有包中的 UWP 应用程序。

```dbgcmd
.terminatepackageapp <PLMPackageName> 
```

例如：

```dbgcmd
.terminatepackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**后台任务**

**.activatepackagebgtask**

.Activatepackagebgtask 命令启用调试，并启动 UWP 后台任务。

```dbgcmd
 .activatepackagebgtask <PLMPackageName> <bgTaskId>
```

例如：

```dbgcmd
.activatepackagebgtask Microsoft.SDKSamples.BackgroundTask.CPP_1.0.0.0_x64__8wekyb3d8bbwe {C05806B1-9647-4765-9A0F-97182CEA5AAD}
```

## <a name="span-idusageexamplesspanspan-idusageexamplesspanspan-idusageexamplesspanusage-examples"></a><span id="Usage_Examples"></span><span id="usage_examples"></span><span id="USAGE_EXAMPLES"></span>用法示例


**您的应用程序启动时附加调试器**

假设您有应用程序名是在名为 e24caf14-8483-4743-b80c-ca46c28c75df 包中的 HelloWorld\_1.0.0.0\_x86\_\_97ghe447vaan8。 验证您的包已安装： 显示完整的名称，并正在运行状态的所有已安装的包。 在命令提示符窗口中，输入以下命令。 CTRL + F 可用于搜索的 HelloWorld 应用程序名称的命令输出。

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

使用.createpackageapp 启动并附加到应用。 .Createpackageapp 命令还启用应用程序的调试。

```dbgcmd
.createpackageapp e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8 App
```

完成调试后，减少使用.disablepackagedebug 命令的包的调试引用计数。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**将调试器附加到已运行的应用**

假设你想要将 WinDbg 附加到 MyApp，已在运行。 在 WinDbg 中，在**文件**菜单中，选择**附加到进程**。 请注意 MyApp 的进程 ID。 让我们假设的进程 ID 是 4816。 递增包含 MyApp 的包的调试引用计数。

```dbgcmd
.enablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

在 WinDbg 中，在**附加到进程**对话框中，选择进程 4816，并单击确定。 WinDbg 将附加到 MyApp。

完成调试后，减少使用.disablepackagedebug 命令的包的调试引用计数。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

**手动挂起和继续您的应用程序**

按照以下步骤手动暂停和恢复您的应用程序。 首先，递增包含您的应用程序的包的调试引用计数。

```dbgcmd
.enablepackagedebug  e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

挂起包。 您的应用程序的挂起调用处理程序，这可能会有所帮助调试。

```dbgcmd
.suspendpackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

完成调试后，恢复包。

```dbgcmd
.resumepackage e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

最后，减小包的调试引用计数。

```dbgcmd
.disablepackagedebug e24caf14-8483-4743-b80c-ca46c28c75df_1.0.0.0_x86__97ghe447vaan8
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 WinDbg 进行调试](debugging-using-windbg.md)

 

 






