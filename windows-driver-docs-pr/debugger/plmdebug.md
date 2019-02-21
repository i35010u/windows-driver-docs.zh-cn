---
title: PLMDebug
description: PLMDebug.exe 是一种工具，可以使用 Windows 调试器来调试进程生命周期管理 (PLM) 下运行的 Windows 应用。
ms.assetid: 68BE8F5D-6425-43E2-B5BC-C1D35614AB32
keywords:
- PLMDebug Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PLMDebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fab398b359d46a8c2147c2d3d67994a236ee4f52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522752"
---
# <a name="plmdebug"></a>PLMDebug


PLMDebug.exe 是一种工具，可以使用 Windows 调试器来调试进程生命周期管理 (PLM) 下运行的 Windows 应用。 PLMDebug，与可能需要手动控制的挂起、 恢复和终止一个 Windows 应用程序。

**提示**  使用 Windows 10，版本 1607年或更高版本，可以使用 UWP 命令，如.createpackageapp 调试 UWP 应用。 有关详细信息请参阅[调试 UWP 应用使用 WinDbg](debugging-a-uwp-app-using-windbg.md)。

 

**从中获取 PLMDebug**

中包含 PLMDebug.exe[有关 Windows 调试工具](index.md)。

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
plmdebug /activateBgTaskTaskId
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Package"></span><span id="_______package"></span><span id="_______PACKAGE"></span> *Package*  
包或正在运行的进程的 ID 的完整名称。

<span id="_______DebuggerCommandLine"></span><span id="_______debuggercommandline"></span><span id="_______DEBUGGERCOMMANDLINE"></span> *DebuggerCommandLine*  
若要打开调试程序命令行。 命令行必须包含到调试器的完整路径。 如果该路径包含空格，则必须放在引号中。 命令行还可以包含参数。 下面提供了一些示例：

`"C:\Program Files (x86)\Windows Kits\8.0\Debuggers\x64\WinDbg.exe"`

`"\"C:\Program Files\Debugging Tools for Windows (x64)\WinDbg.exe\" -server npipe:pipe=test"`

<span id="________query_Package"></span><span id="________query_package"></span><span id="________QUERY_PACKAGE"></span> **/ 查询** \[*包*\]  
显示已安装的包的运行状态。 如果*包*未指定，则此命令将显示所有已安装的包的运行状态。

<span id="________enableDebug_Package_DebuggerCommandLine"></span><span id="________enabledebug_package_debuggercommandline"></span><span id="________ENABLEDEBUG_PACKAGE_DEBUGGERCOMMANDLINE"></span> **/enableDebug** *Package* \[*DebuggerCommandLine*\]  
递增包调试引用计数。 如果它具有非零值调试，包将采用 PLM 策略引用计数。 每次调用**通过 /enableDebug**必须通过调用配对 /**disableDebug**。 如果指定*DebuggerCommandLine*，调试器将复制包从任何应用程序启动时。

<span id="________terminate_Package"></span><span id="________terminate_package"></span><span id="________TERMINATE_PACKAGE"></span> **/terminate** *包*  
终止一个包。

<span id="________forceTerminate_Package"></span><span id="________forceterminate_package"></span><span id="________FORCETERMINATE_PACKAGE"></span> **/forceTerminate** *Package*  
包的强制终止。

<span id="________cleanTerminate_Package"></span><span id="________cleanterminate_package"></span><span id="________CLEANTERMINATE_PACKAGE"></span> **/cleanTerminate** *Package*  
挂起，然后终止包。

<span id="________suspend_Package"></span><span id="________suspend_package"></span><span id="________SUSPEND_PACKAGE"></span> **/suspend** *Package*  
挂起包。

<span id="________resume_Package"></span><span id="________resume_package"></span><span id="________RESUME_PACKAGE"></span> **/resume** *Package*  
恢复包。

<span id="________disableDebug_Package"></span><span id="________disabledebug_package"></span><span id="________DISABLEDEBUG_PACKAGE"></span> **/disableDebug** *Package*  
递减调试引用计数的包。

<span id="________enumerateBgTasksPackage"></span><span id="________enumeratebgtaskspackage"></span><span id="________ENUMERATEBGTASKSPACKAGE"></span> **/enumerateBgTasks***Package*  
枚举包的后台任务 id。

<span id="________activateBgTaskTaskId"></span><span id="________activatebgtasktaskid"></span><span id="________ACTIVATEBGTASKTASKID"></span> **/activateBgTask***TaskId*  
激活后台任务。 请注意，可使用 PLMDebug 激活并不是所有后台任务。

<a name="remarks"></a>备注
-------

必须调用**plmdebug 通过 /enableDebug**在挂起的任何调用之前，恢复或终止函数。

PLMDebug 工具调用的方法[IPackageDebugSettings 接口](https://go.microsoft.com/fwlink/p/?LinkID=267918)。 此接口，可手动控制您的应用程序的进程生命周期管理。 通过此接口 （和结果，通过此工具），可以暂停、 继续和终止您的 Windows 应用程序。 请注意的方法[IPackageDebugSettings 接口](https://go.microsoft.com/fwlink/p/?LinkID=267918)将应用于整个包。 挂起、 继续和终止所有当前包中运行应用程序的影响。

<a name="examples"></a>示例
--------

**示例 1**

**您的应用程序启动时附加调试器**

假设具有名为 MyApp 的名为 MyApp 的包中的应用\_1.0.0.0\_x64\_\_tnq5r49etfg3c。 验证您的包已安装： 显示完整的名称，并正在运行状态的所有已安装的包。 在命令提示符窗口中，输入以下命令。

**plmdebug /query**

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

增加对包的调试引用计数，并指定你想 WinDbg 附加您的应用程序启动时。

**plmdebug /enableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c "C:\\Program Files (x86)\\Windows Kits\\8.0\\Debuggers\\x64\\WinDbg.exe"**

当启动您的应用程序时，WinDbg 将附加并中断。

完成调试后，将调试器分离。 然后递减为您的包的调试引用计数。

**plmdebug /disableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

**示例 2**

**将调试器附加到已运行的应用**

假设你想要将 WinDbg 附加到 MyApp，已在运行。 在 WinDbg 中，在**文件**菜单中，选择**附加到进程**。 请注意 MyApp 的进程 ID。 让我们假设的进程 ID 是 4816。

递增包含 MyApp 的包的调试引用计数。

**plmdebug /enableDebug 4816**

在 WinDbg 中，在**附加到进程**对话框中，选择进程 4816，并单击**确定**。 WinDbg 将附加到 MyApp。

完成调试 MyApp，分离调试程序。 然后递减包的调试引用计数。

**plmdebug /disableDebug 4816**

**示例 3**

**手动挂起和继续您的应用程序**

假设你想要手动挂起和继续您的应用程序。 首先，递增包含您的应用程序的包的调试引用计数。

**plmdebug /enableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

挂起包。 您的应用程序的挂起调用处理程序，这可能会有所帮助调试。

**plmdebug /suspend MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

完成调试后，恢复包。

**plmdebug /resume MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

最后，减小包的调试引用计数。

**plmdebug /disableDebug MyApp\_1.0.0.0\_x64\_\_tnq5r49etfg3c**

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[如何在触发挂起、 继续和后台事件在 Windows 应用中](https://go.microsoft.com/fwlink/p/?LinkID=267916)

[Windows 调试工具中包含的工具](extra-tools.md)

 

 






