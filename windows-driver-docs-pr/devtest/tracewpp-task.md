---
title: TraceWPP 任务
description: Windows Driver Kit (WDK) 提供 TraceWPP 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 tracewpp.exe 工具。
ms.assetid: 74CE1912-8D1D-417E-8B29-36B2AB0253EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 908b3fe9a66ae0b216d6c1c4f8312d0e19f4189a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350284"
---
# <a name="tracewpp-task"></a>TraceWPP 任务


Windows Driver Kit (WDK) 提供 TraceWPP 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 tracewpp.exe 工具。 Tracewpp.exe 工具用于实现[WPP 软件跟踪](wpp-software-tracing.md)。

WppEnabled 是新的元数据，则启用跟踪源文件的 ClCompile 项。 Wpp 任务运行整个 ClCompile 项集合并为 WppEnabled 元数据设置为每个项调用 tracewpp.exe **，则返回 TRUE**。

ClCompile 项目中添加了 WppEnabled 元数据，因为 WPP 任务在 CL 任务，在此事例.c、.cpp 和.h 文件中具有相同类型的输入文件上运行。

**请注意**通过在项目文件中使用 ClCompile 项目访问 tracewpp 的项元数据。 MSBuild 使用在内部在目标内的 TraceWpp 项来将其传递给该任务。

 

下面的示例显示了如何编辑.vcxproj 文件中的元数据。

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

将命令行调用：

```
tracewpp.exe  km /Ic:\test\b.c
tracewpp.exe  dll test2.c
```

上面的示例显示，MSBuild 会调用**tracewpp.exe** b.c 和 test2.c 上仅因为**WppEnabled**元数据设置为**TRUE**这些输入。 此外请注意，这些两个输入的元数据不同。 因此，开关也将不同的这些输入。 换而言之，可以调用具有其自己的元数据集的每个输入。

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
<th align="left">工具开关</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>源</strong>
<p>必需的 ITaskItem [] 参数。 指定源文件的列表。</p></td>
<td align="left">@(TraceWpp)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>AddAlternateNameToMessageGUID</strong>
<p>可选的字符串参数。 指定来自此跟踪提供程序的消息的消息的 GUID 的备选友好名称。</p></td>
<td align="left">%(TraceWpp.WppAddAlternateNameToMessageGUID)</td>
<td align="left"><strong>-o:</strong><em>字符串</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>AdditionalConfigurationFile</strong>
<p>可选的字符串参数。 指定的其他配置文件。 WPP 除了默认文件中，使用指定的文件 defaultwpp.ini。</p></td>
<td align="left">%(TraceWpp.WppAdditionalConfigurationFile)</td>
<td align="left"><strong>-ini:</strong><em>路径</em></td>
</tr>
<tr class="even">
<td align="left"><strong>AdditionalIncludeDirectories</strong>
<p>可选 string [] 参数。 将目录添加到 WPP 搜索包含文件的目录的列表。</p></td>
<td align="left">%(TraceWpp.WppAdditionalIncludeDirectories)</td>
<td align="left"><strong>-I</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>AlternateConfigurationFile</strong>
<p>可选的字符串参数。 指定的备用配置文件。 WPP 而不是 defaultwpp.ini 文件使用此文件。</p></td>
<td align="left">%(TraceWpp.WppAlternateConfigurationFile)</td>
<td align="left"><strong>-defwpp:</strong><em>路径</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateUsingTemplateFile</strong>
<p>可选的字符串参数。 有关 WPP 进程指定的大括号之间的名称与每个源文件{}，WPP 创建另一个文件扩展名的指定的文件的名称。</p></td>
<td align="left">%(TraceWpp.WppGenerateUsingTemplateFile)</td>
<td align="left"><strong>-gen{</strong><em>File.tpl</em><strong>}*.ext</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>可选布尔参数。 如果值为<strong>，则返回 TRUE</strong>，WPP 执行跟踪的增量生成。 否则，WPP 执行重新生成。</p></td>
<td align="left">%(TraceWpp.WppMinimalRebuildFromTracking)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>NumericBaseForFormatStrings</strong>
<p>可选 int 参数。 将生成编号格式字符串的数值的基准。</p></td>
<td align="left">%(TraceWpp.WppNumericBaseForFormatStrings)</td>
<td align="left"><strong>-argbase:</strong><em>数</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>AddControlGUID</strong>
<p>可选的字符串参数。 定义指定控件的 GUID 的 WPP_CONTROL_GUIDS 宏和 WPP_DEFINE_BIT 条目名为 Error、 异常和噪声。</p></td>
<td align="left">%(TraceWpp.WppAddControlGUID)</td>
<td align="left"><strong>-ctl:</strong><em>GUID</em></td>
</tr>
<tr class="even">
<td align="left"><strong>AdditionalOptions</strong>
<p>可选的字符串参数。 命令行选项的列表。</p></td>
<td align="left">%(TraceWpp.WppAdditionalOptions)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>ConfigurationDirectories</strong>
<p>可选 string [] 参数。 指定的配置和模板文件的位置。</p></td>
<td align="left">%(TraceWpp.WppConfigurationDirectories)</td>
<td align="left"><strong>-cfgdir:</strong><em>[Path]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>DllMacro</strong>
<p>可选布尔参数。 定义 WPP_DLL 宏。</p></td>
<td align="left">%(TraceWpp.WppDllMacro)</td>
<td align="left"><strong>-dll</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>FileExtensions</strong>
<p>可选 string [] 参数。 为源文件指定 WPP 可识别的文件类型。 WPP 将忽略具有不同的文件扩展名的文件。</p></td>
<td align="left">%(TraceWpp.WppFileExtensions)</td>
<td align="left"><strong>-ext:</strong><em>.ext1 [.ext2]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>IgnoreExclamationmarks</strong>
<p>可选布尔参数。 指示 WPP 忽略感叹号，也称为 shrieks，使用在复杂的格式，如 %！ 时间戳 ！ %。</p></td>
<td align="left">%(TraceWpp.WppIgnoreExclamationmarks)</td>
<td align="left"><strong>-noshrieks</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>KernelMode</strong>
<p>可选布尔参数。 定义跟踪内核模式组件的 WPP_KERNEL_MODE 宏。 默认情况下，要跟踪仅用户模式组件。</p></td>
<td align="left">%(TraceWpp.WppKernelMode)</td>
<td align="left"><strong>-km</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>OutputDirectory</strong>
<p>可选的字符串参数。 指定 WPP 创建的输出文件的目录。</p></td>
<td align="left">%(TraceWpp.WppOutputDirectory)</td>
<td align="left"><strong>-odir:</strong><em>路径</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>PreprocessorDefinitions</strong>
<p>可选 string [] 参数。 定义源文件的预处理符号。</p></td>
<td align="left">%(TraceWpp.WppPreprocessorDefinitions)</td>
<td align="left"><strong>/D</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>PreserveExtensions</strong>
<p>可选 string [] 参数。 创建 TMH 文件时保留指定的文件扩展名。</p></td>
<td align="left">%(TraceWpp.WppPreserveExtensions)</td>
<td align="left"><strong>-preserveext:</strong><em>ext1[,ext2]</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>ScanConfigurationData</strong>
<p>可选的字符串参数。 配置数据，例如自定义数据类型，以及 defaultwpp.ini 不是配置文件的文件中搜索。</p></td>
<td align="left">%(TraceWpp.WppScanConfigurationData)</td>
<td align="left"><strong>-扫描：</strong><em>文件</em></td>
</tr>
<tr class="even">
<td align="left"><strong>SearchString</strong>
<p>可选的字符串参数。 指示 WPP 搜索要启动跟踪的指定字符串的源代码文件。</p></td>
<td align="left">%(TraceWpp.WppSearchString)</td>
<td align="left"><strong>-lookfor:</strong><em>字符串</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>ToolPath</strong>
<p>可选的字符串参数。 可以指定该工具所在的文件夹的完整路径。</p></td>
<td align="left">$(WPPToolPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TraceFunction</strong>
<p>可选 string [] 参数。 指定用于生成跟踪消息的函数。</p></td>
<td align="left">%(TraceWpp.WppTraceFunction)</td>
<td align="left"><strong>-f u n c:</strong><em>显</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>可选的字符串参数。 若要编写 tlog 的跟踪器日志目录。</p></td>
<td align="left">%(TraceWpp.WppTrackerLogDirectory)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackFileAccess</strong>
<p>可选布尔参数。 如果为 true，则跟踪文件访问模式，此任务。</p></td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPP 预处理器](wpp-preprocessor.md)

[WPP 软件跟踪](wpp-software-tracing.md)

 

 






