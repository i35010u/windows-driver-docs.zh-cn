---
title: TraceWPP 任务
description: Windows 驱动程序工具包 (WDK) 提供 TraceWPP 任务，以便在使用 MSBuild 构建驱动程序时可以运行 tracewpp.exe 工具。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e669edcdbdaff8fe46064412d5003149e748a18c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838091"
---
# <a name="tracewpp-task"></a>TraceWPP 任务


Windows 驱动程序工具包 (WDK) 提供 TraceWPP 任务，以便在使用 MSBuild 构建驱动程序时可以运行 tracewpp.exe 工具。 tracewpp.exe 工具用于实现 [WPP 软件跟踪](wpp-software-tracing.md)。

WppEnabled 是为源文件启用跟踪的 ClCompile 项的新元数据。 此 Wpp 任务通过整个 ClCompile 项集合运行，并为 WppEnabled 元数据设置为 **TRUE** 的每个项调用 tracewpp.exe。

WppEnabled 元数据已添加到 ClCompile 项，因为 WPP 任务在与 CL 任务相同的输入文件类型（在本例中为 c、.cpp 和 .h 文件）运行。

**注意**  通过使用项目文件中的 ClCompile 项，可以访问 tracewpp 的项元数据。 MSBuild 在内部使用 TraceWpp 项以将其传递给任务。

 

下面的示例演示如何在 .vcxproj 文件中编辑元数据。

```XML
<ItemGroup>
    <ClCompile Include="a.c" />
      <WppEnabled>false</WppEnabled>
    <ClCompile Include="b.c">
        <WppEnabled>true</WppEnabled>
        <WppKernelMode>true</WppKernelMode>
        <WppAdditionalIncludeDirectories>c:\test\</WppAdditionalIncludeDirectories>
    </ClCompile>
    <ClCompile Include="test1.c" />
    <ClCompile Include="test2.c">
        <WppEnabled>true</WppEnabled>
        <WppDllMacro>true</WppDllMacro>
    </ClCompile>
</ItemGroup>
```

命令行调用将为：

```
tracewpp.exe  km /Ic:\test\b.c
tracewpp.exe  dll test2.c
```

上面的示例显示 MSBuild 仅在 test2 和上调用 **tracewpp.exe** ，因为这些输入的 **WppEnabled** 元数据设置为 **TRUE** 。 另请注意，这两个输入的元数据是不同的。 因此，这些输入的开关也将有所不同。 换句话说，你可以调用每个输入及其自身的元数据集。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具切换</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>渠道</strong>
<p>所需的 ITaskItem [] 参数。 指定源文件的列表。</p></td>
<td align="left">@ (TraceWpp) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>AddAlternateNameToMessageGUID</strong>
<p>可选的字符串参数。 为来自此跟踪提供程序的消息的消息 GUID 指定替代友好名称。</p></td>
<td align="left">% (TraceWpp. WppAddAlternateNameToMessageGUID) </td>
<td align="left"><strong>-o：</strong><em>String</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>AdditionalConfigurationFile</strong>
<p>可选的字符串参数。 指定附加配置文件。 WPP 除了默认文件 defaultwpp.ini 之外，还使用指定的文件。</p></td>
<td align="left">% (TraceWpp. WppAdditionalConfigurationFile) </td>
<td align="left"><strong>-ini：</strong><em>路径</em></td>
</tr>
<tr class="even">
<td align="left"><strong>AdditionalIncludeDirectories</strong>
<p>可选 string [] 参数。 将目录添加到 WPP 搜索包含文件的目录列表。</p></td>
<td align="left">% (TraceWpp. WppAdditionalIncludeDirectories) </td>
<td align="left"><strong>-I</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>AlternateConfigurationFile</strong>
<p>可选的字符串参数。 指定另一个配置文件。 WPP 使用此文件而不是 defaultwpp.ini 文件。</p></td>
<td align="left">% (TraceWpp. WppAlternateConfigurationFile) </td>
<td align="left"><strong>-defwpp：</strong><em>Path</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateUsingTemplateFile</strong>
<p>可选的字符串参数。 对于每个具有在大括号之间指定名称的进程的源文件 {} ，wpp 会创建另一个具有指定文件扩展名的文件。</p></td>
<td align="left">% (TraceWpp. WppGenerateUsingTemplateFile) </td>
<td align="left"><strong>-gen {</strong><em>File. tpl</em><strong>} * ext</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>可选的布尔参数。 如果该值为 <strong>TRUE</strong>，则 WPP 执行跟踪的增量生成。 否则，WPP 将执行重新生成。</p></td>
<td align="left">% (TraceWpp. WppMinimalRebuildFromTracking) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>NumericBaseForFormatStrings</strong>
<p>可选 int 参数。 为格式字符串的编号建立数字基数。</p></td>
<td align="left">% (TraceWpp. WppNumericBaseForFormatStrings) </td>
<td align="left"><strong>-argbase：</strong><em>Number</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>AddControlGUID</strong>
<p>可选的字符串参数。 定义一个 WPP_CONTROL_GUIDS 宏，其中包含指定的控件 GUID 和名为 "Error"、"异常" 和 "干扰" 的 WPP_DEFINE_BIT 条目。</p></td>
<td align="left">% (TraceWpp. WppAddControlGUID) </td>
<td align="left"><strong>-ctl：</strong><em>GUID</em></td>
</tr>
<tr class="even">
<td align="left"><strong>其他</strong>
<p>可选的字符串参数。 命令行选项列表。</p></td>
<td align="left">% (TraceWpp. WppAdditionalOptions) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>ConfigurationDirectories</strong>
<p>可选 string [] 参数。 指定配置文件和模板文件的位置。</p></td>
<td align="left">% (TraceWpp. WppConfigurationDirectories) </td>
<td align="left"><strong>-cfgdir：</strong><em>[路径]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>DllMacro</strong>
<p>可选的布尔参数。 定义 WPP_DLL 宏。</p></td>
<td align="left">% (TraceWpp. WppDllMacro) </td>
<td align="left"><strong>-dll</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>FileExtensions</strong>
<p>可选 string [] 参数。 指定 WPP 识别为源文件的文件类型。 WPP 将忽略具有不同文件扩展名的文件。</p></td>
<td align="left">% (TraceWpp. WppFileExtensions) </td>
<td align="left"><strong>-ext：</strong><em>. ext1 [. ext2]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>IgnoreExclamationmarks</strong>
<p>可选的布尔参数。 指示 WPP 忽略复杂格式设置中使用的感叹号（也称为 "shrieks"），如%！ timestamp！%。</p></td>
<td align="left">% (TraceWpp. WppIgnoreExclamationmarks) </td>
<td align="left"><strong>-noshrieks</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>KernelMode</strong>
<p>可选的布尔参数。 定义跟踪内核模式组件的 WPP_KERNEL_MODE 宏。 默认情况下，只跟踪用户模式组件。</p></td>
<td align="left">% (TraceWpp. WppKernelMode) </td>
<td align="left"><strong>-公里</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>OutputDirectory</strong>
<p>可选的字符串参数。 指定 WPP 创建的输出文件的目录。</p></td>
<td align="left">% (TraceWpp. WppOutputDirectory) </td>
<td align="left"><strong>-odir：</strong><em>Path</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>PreprocessorDefinitions</strong>
<p>可选 string [] 参数。 定义源文件的预处理符号。</p></td>
<td align="left">% (TraceWpp. WppPreprocessorDefinitions) </td>
<td align="left"><strong>/D</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>PreserveExtensions</strong>
<p>可选 string [] 参数。 创建 TMH 文件时，保留指定的文件扩展名。</p></td>
<td align="left">% (TraceWpp. WppPreserveExtensions) </td>
<td align="left"><strong>-preserveext：</strong><em>ext1 [，ext2]</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>ScanConfigurationData</strong>
<p>可选的字符串参数。 在不是配置文件的文件以及 defaultwpp.ini 中搜索配置数据（如自定义数据类型）。</p></td>
<td align="left">% (TraceWpp. WppScanConfigurationData) </td>
<td align="left"><strong>-scan：</strong><em>File</em></td>
</tr>
<tr class="even">
<td align="left"><strong>SearchString</strong>
<p>可选的字符串参数。 指示 WPP 搜索指定字符串的源文件以启动跟踪。</p></td>
<td align="left">% (TraceWpp. WppSearchString) </td>
<td align="left"><strong>-lookfor：</strong><em>String</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>ToolPath</strong>
<p>可选的字符串参数。 允许您指定该工具所在的文件夹的完整路径。</p></td>
<td align="left">$ (WPPToolPath) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TraceFunction</strong>
<p>可选 string [] 参数。 指定随后可用于生成跟踪消息的函数。</p></td>
<td align="left">% (TraceWpp. WppTraceFunction) </td>
<td align="left"><strong>-func：</strong><em>FunctionDescription</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>可选的字符串参数。 用于跟踪程序的日志目录，用于编写 tlog。</p></td>
<td align="left">% (TraceWpp. WppTrackerLogDirectory) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackFileAccess</strong>
<p>可选的布尔参数。 如果为 true，则跟踪此任务的文件访问模式。</p></td>
<td align="left">$ (TrackFileAccess) </td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPP 预处理器](wpp-preprocessor.md)

[WPP 软件跟踪](wpp-software-tracing.md)

 

 






