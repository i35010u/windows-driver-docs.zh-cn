---
title: PLMDebug
description: PLMDebug.exe 是一种工具，使您可以使用 Windows 调试器调试 Windows 应用程序，该应用程序在进程生命周期管理 (PLM) 下运行。
ms.assetid: 68BE8F5D-6425-43E2-B5BC-C1D35614AB32
keywords:
- PLMDebug Windows 调试
ms.date: 06/03/2020
topic_type:
- apiref
api_name:
- PLMDebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c827e7f6ec2874f538a75a5ff09da6e1e5161503
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253109"
---
# <a name="plmdebug"></a>PLMDebug

PLMDebug.exe 是一种工具，使您可以使用 Windows 调试器调试 Windows 应用程序，该应用程序在进程生命周期管理 (PLM) 下运行。 使用 PLMDebug，可以手动控制挂起、继续和终止 Windows 应用。

**提示**   使用 Windows 10 版本1607或更高版本，可以使用 UWP 命令（如 createpackageapp）调试 UWP 应用。 有关详细信息，请参阅 [使用 WinDbg 调试 UWP 应用](debugging-a-uwp-app-using-windbg.md)。

**从何处获取 PLMDebug**

PLMDebug.exe 包含在 [Windows 调试工具](index.md)中。

```console
plmdebug /query [Package]
plmdebug /enableDebug Package [DebuggerCommandLine]
plmdebug /terminate Package
plmdebug /forceterminate Package
plmdebug /cleanterminate Package
plmdebug /suspend Package
plmdebug /resume Package
plmdebug /disableDebug Package
plmdebug /enumerateBgTasks Package
plmdebug /activateBgTaskTaskId "{TaskID}"
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______Package"></span><span id="_______package"></span><span id="_______PACKAGE"></span>*包*  
包的完整名称或正在运行的进程的 ID。

<span id="_______DebuggerCommandLine"></span><span id="_______debuggercommandline"></span><span id="_______DEBUGGERCOMMANDLINE"></span>*DebuggerCommandLine*  
用于打开调试器的命令行。 命令行必须包含调试器的完整路径。 如果路径包含空格，则必须用引号将其引起来。 命令行也可以包含参数。 下面是一些示例：

`"C:\Program Files (x86)\Windows Kits\8.0\Debuggers\x64\WinDbg.exe"`

`"\"C:\Program Files\Debugging Tools for Windows (x64)\WinDbg.exe\" -server npipe:pipe=test"`

<span id="________query_Package"></span><span id="________query_package"></span><span id="________QUERY_PACKAGE"></span>**/query** \[*包*\]  
显示已安装包的运行状态。 如果未指定 *Package* ，此命令将显示所有已安装包的运行状态。

<span id="________enableDebug_Package_DebuggerCommandLine"></span><span id="________enabledebug_package_debuggercommandline"></span><span id="________ENABLEDEBUG_PACKAGE_DEBUGGERCOMMANDLINE"></span>**/enableDebug** *包* \[ *DebuggerCommandLine*\]  
递增包的调试引用计数。 如果包具有非零的调试引用计数，则从 PLM 策略中免除。 对 **/enableDebug** 的每次调用都必须与对/**disableDebug**的调用配对。 如果指定 *DebuggerCommandLine*，则在启动包的任何应用时，调试器将附加。

<span id="________terminate_Package"></span><span id="________terminate_package"></span><span id="________TERMINATE_PACKAGE"></span>**/Terminate** *包*  
终止包。

<span id="________forceTerminate_Package"></span><span id="________forceterminate_package"></span><span id="________FORCETERMINATE_PACKAGE"></span>**/ForceTerminate** *包*  
强制终止包。

<span id="________cleanTerminate_Package"></span><span id="________cleanterminate_package"></span><span id="________CLEANTERMINATE_PACKAGE"></span>**/CleanTerminate** *包*  
挂起然后终止包。

<span id="________suspend_Package"></span><span id="________suspend_package"></span><span id="________SUSPEND_PACKAGE"></span>**/Suspend** *包*  
挂起包。

<span id="________resume_Package"></span><span id="________resume_package"></span><span id="________RESUME_PACKAGE"></span>**/Resume** *包*  
恢复包。

<span id="________disableDebug_Package"></span><span id="________disabledebug_package"></span><span id="________DISABLEDEBUG_PACKAGE"></span>**/DisableDebug** *包*  
减少包的调试引用计数。

<span id="________enumerateBgTasksPackage"></span><span id="________enumeratebgtaskspackage"></span><span id="________ENUMERATEBGTASKSPACKAGE"></span>**/EnumerateBgTasks** *包*  
枚举包的后台任务 id。

<span id="________activateBgTaskTaskId"></span><span id="________activatebgtasktaskid"></span><span id="________ACTIVATEBGTASKTASKID"></span>**/activateBgTask**"{*TaskId*}"  
激活后台任务。 请注意，并非所有后台任务都可以使用 PLMDebug 激活。 TaskID 必须用大括号和引号括起来。 例如：

`plmdebug.exe /activatebgtask "{29421c11-1e1a-47a4-9121-949ce9e25456}"`

<a name="remarks"></a>备注
-------

调用任何 "挂起"、"继续" 或 "终止" 函数之前，必须先调用 **plmdebug/enableDebug** 。

PLMDebug 工具调用 [IPackageDebugSettings 接口](https://docs.microsoft.com/windows/win32/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)的方法。 利用此接口，你可以对应用程序的流程生命周期管理进行手动控制。 通过此接口 (，因此通过此工具) ，你可以挂起、恢复和终止 Windows 应用程序。 请注意， [IPackageDebugSettings 接口](https://docs.microsoft.com/windows/win32/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings) 的方法适用于整个包。 挂起、继续和终止会影响包中当前正在运行的所有应用。

<a name="examples"></a>示例
--------

**示例 1**

**在应用程序启动时附加调试器**

假设你有一个名为 MyApp 的应用程序，该应用程序在名为 MyApp \_ 1.0.0.0 x64 tnq5r49etfg3c 的包中 \_ \_ \_ 。 通过显示所有已安装的包的完整名称和运行状态，验证是否已安装包。 在命令提示符窗口中，输入以下命令。

**plmdebug/query**

```console
Package full name: 1daa103b-74e1-426d-8193-b6bc7ed66fed_1.0.0.0_x86__tnq5r49etfg3c
Package state: Terminated

Package full name: 41fb5f27-7b60-4f5e-8459-803673131dd9_1.0.0.0_x86__tnq5r49etfg3c
Package state: Suspended
...
Package full name: MyApp_1.0.0.0_x64__tnq5r49etfg3c
Package state: Terminated
...
```

递增包的调试引用计数，并指定在启动应用程序时希望将 WinDbg 附加到。

**plmdebug/enableDebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c "C： \\ Program Files (x86) \\ Windows 工具包 \\ 8.0 \\ 调试器 \\ x64 \\WinDbg.exe"**

当你启动应用程序时，WinDbg 会附加并中断。

完成调试后，分离调试器。 然后，减小包的调试引用计数。

**plmdebug/disableDebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

**示例 2**

**将调试程序附加到已在运行的应用程序**

假设要将 WinDbg 附加到已在运行的 MyApp。 在 WinDbg 的 " **文件** " 菜单上，选择 " **附加到进程**"。 记下 MyApp 的进程 ID。 假设进程 ID 为4816。

为包含 MyApp 的包增加调试引用计数。

**plmdebug/enableDebug 4816**

在 WinDbg 的 " **附加到进程** " 对话框中，选择 "处理 4816"，然后选择 **"确定"**。 WinDbg 将附加到 MyApp。

完成调试 MyApp 后，分离调试器。 然后，减小包的调试引用计数。

**plmdebug/disableDebug 4816**

**示例 3**

**手动暂停和恢复应用**

假设要手动暂停并恢复应用。 首先，请为包含应用的包增加调试引用计数。

**plmdebug/enableDebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

暂停包。 将调用应用的挂起处理程序，这对于调试很有帮助。

**plmdebug/suspend MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

完成调试后，继续执行包。

**plmdebug/resume MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

最后，减小包的调试引用计数。

**plmdebug/disableDebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

**示例 4**

**手动激活后台任务**

若要手动激活用于调试的后台任务，可以查询已注册的后台任务的列表，然后通过 plmdebug 激活该任务。

首先查询已注册的一组后台任务：

**plmdebug/enumeratebgtasks MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**
```console
Package full name is MyApp_1.0.0.0_x64__tnq5r49etfg3c.
Background Tasks:
SampleTask : {50DB0363-D722-4E23-A18F-1EF49B226CC3}
```

如果要保证任务处于激活状态，请先启用调试模式。 例如，当系统处于电池保护状态时，TimeTrigger 激活任务等机会任务将不会激活。 启用包的调试模式将确保系统忽略禁止激活的策略。

**plmdebug/enabledebug MyApp \_ 1.0.0.0 \_ x64 \_ \_ tnq5r49etfg3c**

然后，使用所枚举的注册 GUID 激活所需的任务。

**plmdebug/activatebgtask "{50DB0363-D722-4E23-A18F-1EF49B226CC3}"**

## <a name="see-also"></a>另请参阅

[在 Visual Studio 中调试 UWP 应用时如何触发挂起、继续和后台事件](https://docs.microsoft.com/visualstudio/debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio)

[Windows 调试工具中包含的工具](extra-tools.md)
