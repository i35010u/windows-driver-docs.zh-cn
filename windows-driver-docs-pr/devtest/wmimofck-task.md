---
title: Wmimofck 任务
description: Windows Driver Kit (WDK) 提供了 Wmimofck 任务，以便在生成使用 MSBuild 的驱动程序时，可以运行 wmimofck.exe 工具。
ms.assetid: 33C5C079-510F-4BD3-AEF1-F152E88E45C2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29295c3d39d4c87b1b0bc5a4cd0345d1bc8bca2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519461"
---
# <a name="wmimofck-task"></a>Wmimofck 任务


Windows Driver Kit (WDK) 提供了 Wmimofck 任务，以便在生成使用 MSBuild 的驱动程序时，可以运行 wmimofck.exe 工具。

有关使用 Wmimofck 工具的信息，请参阅[使用 Wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)。

MSBuild 使用 Wmimofck 项发送 Wmimofck 任务的参数。 在项目文件中使用 Wmimofck 项访问 wmimofck 的项元数据。

下面的示例显示了如何编辑.vcxproj 文件中的元数据。

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

下面的示例演示如何在命令提示符窗口中运行 Wmimofck.exe:

```
Wmimofck.exe -u a.bmf
Wmimofck.exe –h"b.h" b.bmf
```

上面的示例调用 wmimofck.exe a.bmf 和 b.bmf，但具有不同的参数集，且不同的元数据。 因此，开关也将不同的这些输入。 换而言之，可以调用具有其自己的元数据集的每个输入。

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
<th align="left">工具开关</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>源</strong>
<p>所需的 ITaskItem 参数。 指定的输入的源文件。</p></td>
<td align="left">@(Wmimofck)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateStructureDefinitionsForDatablocks</strong>
<p>可选布尔参数。 Wmimofck 成员的生成定义具有固定的大小，包括指定 MaxLen 限定符的可选属性的每个属性。</p></td>
<td align="left">%(Wmimofck.GenerateStructureDefinitionsForDatablocks)</td>
<td align="left"><strong>-u</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateStructureDefinitionsForMethodParameters</strong>
<p>可选布尔参数。 标头文件包含的输入和输出的每个 WMI 方法的结构定义。</p></td>
<td align="left">%(Wmimofck.GenerateStructureDefinitionsForMethodParameters)</td>
<td align="left"><strong>-m</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>HeaderOutputFile</strong>
<p>可选的字符串参数。 生成用于使标头文件与 MOF 定义同步的 C 语言头文件 （.h 文件）。</p></td>
<td align="left">%(Wmimofck.HeaderOutputFile)</td>
<td align="left"><strong>-h</strong><em>Filename</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>HexdumpOutputFile</strong>
<p>可选的字符串参数。 生成可以在运行时提供动态 MOF 数据的驱动程序源中包含的.bmf 数据的十六进制版本。</p></td>
<td align="left">%(Wmimofck.HexdumpOutputFile)</td>
<td align="left"><strong>-x</strong><em>Filename</em></td>
</tr>
<tr class="even">
<td align="left"><strong>HTMLUIOutputDirectory</strong>
<p>如果此值设置为 true，则它会生成-w 开关。</p></td>
<td align="left">%(Wmimofck.HTMLUIOutputDirectory)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>HTMLOutputDirectory</strong>
<p>可选的字符串参数。 指定 Wmimofck 生成的 HTML 文件的目录。</p></td>
<td align="left">%(Wmimofck.HTMLOutputDirectory)</td>
<td align="left"><strong>-w</strong><em>Directory</em></td>
</tr>
<tr class="even">
<td align="left"><strong>MFLFile</strong>
<p>可选的字符串参数。 指定包含已修正的类的文件。</p></td>
<td align="left">%(Wmimofck.MFLFile)</td>
<td align="left"><strong>-z</strong><em>MFLFile</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>可选布尔参数。 如果为 true，则执行跟踪的增量生成;如果为 false，则执行重新生成。</p></td>
<td align="left">%(Wmimofck.MinimalRebuildFromTracking)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>MOFFile</strong>
<p>可选的字符串参数。 指定包含独立于语言的 WMI 类声明的文件。</p></td>
<td align="left">%(Wmimofck.MOFFile)</td>
<td align="left"><strong>-y</strong><em>MOFFile</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SourceOutputFile</strong>
<p>可选的字符串参数。 生成一个包含 WMI 驱动程序代码的存根的 C 语言源代码文件。</p></td>
<td align="left">%(Wmimofck.SourceOutputFile)</td>
<td align="left"><strong>-c</strong><em>Filename</em></td>
</tr>
<tr class="even">
<td align="left"><strong>TLogReadFiles</strong>
<p>可选的字符串参数。</p></td>
<td align="left">@(WmimofckTLogReadFiles)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TLogWriteFiles</strong>
<p>可选的字符串参数。</p></td>
<td align="left">@(WmimofckTLogWriteFiles)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolExe</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$(WmimofckToolExe)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>ToolPath</strong>
<p>可选的字符串参数。 指定该工具所在的文件夹的完整路径。</p></td>
<td align="left">$(WmimofckToolPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>可选的字符串参数。 指定跟踪器编写 tlog 的日志目录。</p></td>
<td align="left">%(Wmimofck.TrackerLogDirectory)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackFileAccess</strong>
<p>可选布尔参数。 如果为 true，则跟踪文件访问模式，此任务。</p></td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolArchitecture</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$(WmimofckToolArchitecture)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerFrameworkPath</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$(WmimofckTrackerFrameworkPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackerSdkPath</strong>
<p>可选的字符串参数。</p></td>
<td align="left">$(WmimofckTrackerSdkPath)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>VBScriptTestOutputFile</strong>
<p>可选的字符串参数。 程序创建一个 VBScript，它将查询所有数据块和 MOF 文件中指定的属性。</p></td>
<td align="left">%(Wmimofck.VBScriptTestOutputFile)</td>
<td align="left"><strong>-t</strong><em>Filename</em></td>
</tr>
<tr class="even">
<td align="left"><strong>AdditionalOptions</strong>
<p>可选的字符串参数。</p></td>
<td align="left">%(Wmimofck.AdditionalOptions)</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[使用 Wmimofck.exe](https://msdn.microsoft.com/library/windows/hardware/ff565588)

 

 






