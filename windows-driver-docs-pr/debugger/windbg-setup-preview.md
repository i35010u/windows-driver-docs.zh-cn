---
title: WinDbg 预览-设置和工作区
description: 本部分介绍如何设置 WinDbg 预览调试器。
ms.date: 01/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8f7b6a4d0987326e509aa20a5c82d3d51400f5f4
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256737"
---
# <a name="windbg-preview---settings-and-workspaces"></a>WinDbg 预览-设置和工作区

![带有位模式的 windbg 预览的小徽标](images/windbgx-preview-logo.png)

本部分介绍如何设置和配置 WinDbg 预览调试器。

## <a name="settings"></a>“设置”

使用 "设置" 菜单设置源和符号路径等项，并为调试器选择浅和深色主题。 

![显示 "常规" 选项卡的设置的屏幕截图](images/windbgx-settings-menu.png)

目前有六个设置对话框面板：

- “常规”
- “命令”窗口
- 调试设置
- 反汇编窗口
- 事件 & 异常
- 源窗口

有关设置路径的详细信息，请参阅[在 WinDbg 中](source-window.md)[访问用于调试的符号](accessing-symbols-for-debugging.md)和源代码调试。

## <a name="workspaces"></a>工作区

工作区允许您将配置信息保存在目标连接信息文件中。

工作区中的选项在关闭调试器时保存，或者可以使用*文件* -> *保存工作区*手动保存。 

从 "最近的目标" 列表启动时，将自动加载工作区，也可以在 "文件" 菜单中手动加载工作区。 

除目标连接信息外，以下设置还存储在工作区文件中。

#### <a name="general-settings"></a>常规设置

> [!NOTE]
> 此列表和格式不是最终的，可能会发生更改。

设置 | 默认值 | 描述
--- | --- | ---
FinalBreak |true | 如果为 true，则忽略最后一个断点（-g 命令行选项）。
SourceDebugging |true  | 在源或程序集模式间切换。
DebugChildProcesses | 否| （仅用户模式）如果为 true，则调试由目标应用程序启动的子进程。 （-o 命令行选项）。
Noninvasive | 否  |  指定非侵害性附加（-pv 命令行选项）。
NoDebugHeap | 否  |  指定不应使用调试堆（-hd 命令行选项）。
Verbose | 否  | 当启用详细模式时，某些显示命令（如寄存器转储）会生成更详细的输出。 （-v 命令行选项）。
提升 | - |  WinDbg 在内部使用-不修改。
可重新启动 | - |  WinDbg 在内部使用-不修改。
UseImplicitCommandLine | 否 | 使用隐式命令行（-cimp 命令行选项）。 这将使用隐式命令行（而不是显式进程）来启动调试器。

有关命令行选项的详细信息，请参阅[WinDbg 命令行选项](windbg-command-line-options.md)。

#### <a name="symbol-settings"></a>符号设置

设置 | 默认值 | 描述
--- | --- | ---
SymbolOptionsOverride | 0 | 显式符号选项掩码，采用单个十六进制数的形式。
ShouldOverrideSymbolOptions | 否 | 如果设置为*true* ，则用提供的符号选项掩码替代下面列出的所有符号选项，如上所述。
SymOptExactSymbols | 否 | 此选项使调试器对所有符号文件执行严格的计算。
SymOptFailCriticalErrors | 否 | 此符号选项导致禁止显示文件访问错误对话框。
SymOptIgnoreCvRec | 否 | 在搜索符号时，此选项会导致符号处理程序忽略加载的图像标头中的 CV 记录。 
SymOptIgnoreNtSympath | 否 | 此选项使调试器忽略符号路径和可执行映像路径的环境变量设置。 
SymOptNoCpp | 否 | 此符号选项用于关闭C++转换。 设置此符号选项后，所有符号中的：：替换为 __。 
SymOptNoUnqualifiedLoads | 否 | 此符号选项禁用符号处理程序的自动加载模块。 如果设置了此选项，并且调试器尝试匹配符号，则它将只搜索已加载的模块。 
SymOptAutoPublics | 否 | 此符号选项会使 Dbghelp.dll 仅搜索 .pdb 文件中的公共符号表，作为最后的手段。 如果在搜索私有符号数据时找到任何匹配项，则不会搜索公共符号。 这可提高符号搜索速度。 
SymOptDebug | 否 | 此符号选项用于打开干扰符号加载。 这会指示调试器显示有关其符号搜索的信息。

有关符号选项的详细信息，请参阅[符号选项](symbol-options.md)。

#### <a name="window-layout-settings"></a>窗口布局设置

 窗口布局是全局保存的，不保存在工作区文件中。 

#### <a name="workspaces-xml-file"></a>工作区 XML 文件

工作区和目标连接信息以 XML 格式存储。

以下文件显示了一个示例工作区配置文件。

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

请注意，在将更多功能添加到 WinDbg 预览调试器时，此文件格式将继续演化。

---

## <a name="see-also"></a>另请参阅

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)
