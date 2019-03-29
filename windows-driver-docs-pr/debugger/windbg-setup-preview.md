---
title: WinDbg 预览版-设置和工作区
description: 本部分介绍如何设置 WinDbg 预览调试器。
ms.date: 08/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64cf7cc9d215afc29e332ea6ee5b5a4fa10ab199
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564588"
---
# <a name="windbg-preview---settings-and-workspaces"></a>WinDbg 预览版-设置和工作区

本部分介绍如何设置和配置 WinDbg 预览调试程序。


## <a name="settings"></a>设置

使用设置菜单来设置源和符号路径，以及为调试器选择浅色和深色主题。 

![反馈中心显示反馈选项包括添加新的反馈按钮的屏幕截图](images/windbgx-settings-menu.png)

设置路径的详细信息，请参阅[访问以便进行调试的符号](accessing-symbols-for-debugging.md)并[源代码调试在 WinDbg 中](source-window.md)。

## <a name="workspaces"></a>工作区

工作区允许您将配置信息保存在目标连接信息文件。

工作区中的选项时关闭调试程序保存或可以使用手动保存*文件* -> *保存工作区*。 

从最近的目标列表启动时，会自动加载工作区或可以在文件菜单手动加载它们。 

除了目标连接信息，以下设置存储在工作区文件。

#### <a name="general-settings"></a>常规设置 
> [!NOTE]
> 此列表和格式还没有结束，并且可能会更改。

设置 | 默认 | 描述
--- | --- | ---
FinalBreak |true | 如果为 true，将忽略最终断点 (-g 命令行选项)。
SourceDebugging |true  | 源或程序集模式之间切换。
DebugChildProcesses | false| （仅限用户模式）如果为 true 将调试启动目标应用程序的子进程。 (-o 命令行选项)。
非侵入 | false  |  指定非入侵性附加 (-pv 命令行选项)。
NoDebugHeap | false  |  指定不应使用调试堆 (-hd 命令行选项)。
Verbose | false  | 启用详细模式后，某些显示的命令 （例如注册转储） 生成更详细的输出。 (-v 命令行选项)。
提升 | - |  在内部使用 WinDbg-不要修改。
可重新启动 | - |  在内部使用 WinDbg-不要修改。
UseImplicitCommandLine | false | 隐式使用命令行 (-cimp 命令行选项)。 这将使用隐式的命令行，而不是一个显式的过程以运行启动调试器。

有关命令行选项的详细信息，请参阅[WinDbg 命令行选项](windbg-command-line-options.md)。


#### <a name="symbol-settings"></a>符号设置 

设置 | 默认 | 描述
--- | --- | ---
SymbolOptionsOverride | 0 | 显式符号选项掩码，一个十六进制数字的形式。
ShouldOverrideSymbolOptions | false | 如果设置为 *，则返回 true*替代所有符号选项下面列出了提供的符号选项掩码，上面所述。
SymOptExactSymbols | false | 此选项会导致调试器执行的所有符号文件严格评估。
SymOptFailCriticalErrors | false | 此符号选项将导致文件访问错误对话框来禁止显示。
SymOptIgnoreCvRec | false | 此选项会导致要搜索的符号时忽略 CV 记录加载的映像标头中的符号处理程序。 
SymOptIgnoreNtSympath | false | 此选项会导致调试器忽略符号路径和可执行映像路径的环境变量设置。 
SymOptNoCpp | false | 此符号选项将关闭 c + + 转换。 当设置此符号选项时，:: 替换为 __ 中的所有符号。 
SymOptNoUnqualifiedLoads | false | 此符号选项禁用符号处理程序的自动加载模块。 如果设置此选项，调试器会尝试匹配一个符号，它将仅搜索已加载的模块。 
SymOptAutoPublics | false | 此符号选项将导致 DbgHelp 公共符号表中仅作为最后的手段的.pdb 文件中搜索。 如果找到任何匹配项搜索中的私有符号数据时，将不搜索公共符号。 这提高了符号搜索速度。 
SymOptDebug | false | 此符号选项开启干扰符号加载。 这会指示调试器以显示有关其搜索符号信息。

符号选项的详细信息，请参阅[符号选项](symbol-options.md)。


#### <a name="window-layout-settings"></a>窗口布局设置

 窗口布局全局保存，并且不会保存在工作区文件。 


#### <a name="workspaces-xml-file"></a>工作区 XML 文件

工作区和目标连接信息存储在 XML 格式。 

以下文件中，显示的示例工作区配置文件。

```xml
<?xml version="1.0" encoding="utf-8"?>
<TargetConfig Name="C:\paint.dmp" LastUsed="2017-08-03T21:34:20.1013837Z">
  <EngineConfig />
  <EngineOptions>
    <Property name="FinalBreak" value="true" />
    <Property name="SourceDebugging" value="true" />
    <Property name="DebugChildProcesses" value="false" />
    <Property name="Noninvasive" value="false" />
    <Property name="NoDebugHeap" value="false" />
    <Property name="Verbose" value="false" />
    <Property name="SymbolOptionsOverride" value="0" />
    <Property name="ShouldOverrideSymbolOptions" value="false" />
    <Property name="SymOptExactSymbols" value="false" />
    <Property name="SymOptFailCriticalErrors" value="false" />
    <Property name="SymOptIgnoreCvRec" value="false" />
    <Property name="SymOptIgnoreNtSympath" value="false" />
    <Property name="SymOptNoCpp" value="false" />
    <Property name="SymOptNoUnqualifiedLoads" value="false" />
    <Property name="SymOptAutoPublics" value="false" />
    <Property name="SymOptDebug" value="false" />
    <Property name="Elevate" value="false" />
    <Property name="Restartable" value="true" />
    <Property name="UseImplicitCommandLine" value="false" />
  </EngineOptions>
  <TargetOptions>
    <Option name="OpenDump">
      <Property name="DumpPath" value="C:\paint.dmp" />
    </Option>
  </TargetOptions>
</TargetConfig>
```

请注意，这种文件格式将继续发展更多的功能添加到 WinDbg 预览调试程序。


---

## <a name="see-also"></a>请参阅

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)






