---
title: Wmimofck 任务
description: Windows 驱动程序工具包 (WDK) 提供 Wmimofck 任务，因此，在使用 MSBuild 构建驱动程序时，可以运行 wmimofck.exe 工具。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 442cfef9326e9d1db32072d5ce0db20ce5bb9dda
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810661"
---
# <a name="wmimofck-task"></a>Wmimofck 任务


Windows 驱动程序工具包 (WDK) 提供 Wmimofck 任务，因此，在使用 MSBuild 构建驱动程序时，可以运行 wmimofck.exe 工具。

有关使用 Wmimofck 工具的信息，请参阅 [使用 Wmimofck.exe](../kernel/using-wmimofck-exe.md)。

MSBuild 使用 Wmimofck 项来发送 Wmimofck 任务的参数。 使用项目文件中的 Wmimofck 项访问 wmimofck 的项元数据。

下面的示例演示如何在 .vcxproj 文件中编辑元数据。

```XML
<ItemGroup>
    <Wmimofck Include="a.bmf">
      <GenerateStructureDefinitionsForDatablocks>true</GenerateStructureDefinitionsForDatablocks>
    </Wmimofck>
    <Wmimofck Include="b.bmf">
      <HeaderOutputFile>b.h</HeaderOutputFile>
    </Wmimofck>
</ItemGroup>
```

下面的示例演示如何在命令提示符窗口中运行 Wmimofck.exe：

```
Wmimofck.exe -u a.bmf
Wmimofck.exe –h"b.h" b.bmf
```

上面的示例同时调用 bmf 和 bmf 上的 wmimofck.exe，但使用不同的参数集和不同的元数据。 因此，这些输入的开关也将有所不同。 换句话说，你可以调用每个输入及其自身的元数据集。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Wmimofck 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具切换</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>源程序</strong>
<p>必需的 ITaskItem 参数。 指定输入源文件。</p></td>
<td align="left">@ (Wmimofck) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateStructureDefinitionsForDatablocks</strong>
<p>可选的布尔参数。 Wmimofck 为具有固定大小的每个属性生成成员定义，包括指定 MaxLen 限定符的可选属性。</p></td>
<td align="left">% (Wmimofck. GenerateStructureDefinitionsForDatablocks) </td>
<td align="left"><strong>-u</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateStructureDefinitionsForMethodParameters</strong>
<p>可选的布尔参数。 标头文件包含每个 WMI 方法的输入和输出的结构定义。</p></td>
<td align="left">% (Wmimofck. GenerateStructureDefinitionsForMethodParameters) </td>
<td align="left"><strong>-m</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>HeaderOutputFile</strong>
<p>可选的字符串参数。 生成一个 C 语言标头文件 ( .h 文件) 然后可以使用该文件来使标头文件与 MOF 定义保持同步。</p></td>
<td align="left">% (Wmimofck. HeaderOutputFile) </td>
<td align="left"><strong>-h</strong><em>Filename</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>HexdumpOutputFile</strong>
<p>可选的字符串参数。 生成可包含在驱动程序源中的 bmf 数据的十六进制版本，以便在运行时提供动态 MOF 数据。</p></td>
<td align="left">% (Wmimofck. HexdumpOutputFile) </td>
<td align="left"><strong>-x</strong><em>Filename</em></td>
</tr>
<tr class="even">
<td align="left"><strong>HTMLUIOutputDirectory</strong>
<p>如果此值设置为 true，则生成-w 开关。</p></td>
<td align="left">% ( # B0 LUIOutputDirectory) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>HTMLOutputDirectory</strong>
<p>可选的字符串参数。 指定 Wmimofck 生成的 HTML 文件的目录。</p></td>
<td align="left">% ( # B0 LOutputDirectory) </td>
<td align="left"><strong>-w</strong><em>目录</em></td>
</tr>
<tr class="even">
<td align="left"><strong>MFLFile</strong>
<p>可选的字符串参数。 指定包含修改后的类的文件。</p></td>
<td align="left">% (Wmimofck. MFLFile) </td>
<td align="left"><strong>-z</strong><em>MFLFile</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>可选的布尔参数。 如果为 true，则执行跟踪的增量生成;如果为 false，则执行重新生成。</p></td>
<td align="left">% (Wmimofck. MinimalRebuildFromTracking) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>MOFFile</strong>
<p>可选的字符串参数。 指定包含与语言无关的 WMI 类声明的文件。</p></td>
<td align="left">% (Wmimofck. MOFFile) </td>
<td align="left"><strong>-y</strong><em>MOFFile</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SourceOutputFile</strong>
<p>可选的字符串参数。 生成 C 语言源文件，其中包含用于 WMI 驱动程序代码的存根。</p></td>
<td align="left">% (Wmimofck. SourceOutputFile) </td>
<td align="left"><strong>-c</strong><em>文件名</em></td>
</tr>
<tr class="even">
<td align="left"><strong>TLogReadFiles</strong>
<p>可选的字符串参数。</p></td>
<td align="left">@ (WmimofckTLogReadFiles) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TLogWriteFiles</strong>
<p>可选的字符串参数。</p></td>
<td align="left">@ (WmimofckTLogWriteFiles) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolExe</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$ (WmimofckToolExe) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>ToolPath</strong>
<p>可选的字符串参数。 指定工具所在的文件夹的完整路径。</p></td>
<td align="left">$ (WmimofckToolPath) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>可选的字符串参数。 指定跟踪器用于写入 tlog 的日志目录。</p></td>
<td align="left">% (Wmimofck. TrackerLogDirectory) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackFileAccess</strong>
<p>可选的布尔参数。 如果为 true，则跟踪此任务的文件访问模式。</p></td>
<td align="left">$ (TrackFileAccess) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolArchitecture</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$ (WmimofckToolArchitecture) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerFrameworkPath</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$ (WmimofckTrackerFrameworkPath) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackerSdkPath</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$ (WmimofckTrackerSdkPath) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>VBScriptTestOutputFile</strong>
<p>可选的字符串参数。 将创建一个 VBScript 程序，该程序将查询 MOF 文件中指定的所有数据块和属性。</p></td>
<td align="left">% ( # B0 criptTestOutputFile) </td>
<td align="left"><strong>-t</strong><em>Filename</em></td>
</tr>
<tr class="even">
<td align="left"><strong>其他</strong>
<p>可选的字符串参数。</p></td>
<td align="left">% (Wmimofck. 其他) </td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 Wmimofck.exe](../kernel/using-wmimofck-exe.md)

 

