---
title: Stampinf 任务
description: Windows 驱动程序工具包 (WDK) 提供 StampInf 任务，以便在使用 MSBuild 构建驱动程序时可以运行 stampinf.exe 工具。 有关 stampinf.exe 工具的信息，请参阅 Stampinf。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 010406e156425666aa0dff6df4360c1054932977
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826667"
---
# <a name="stampinf-task"></a>Stampinf 任务


Windows 驱动程序工具包 (WDK) 提供 StampInf 任务，以便在使用 MSBuild 构建驱动程序时可以运行 stampinf.exe 工具。 有关 stampinf.exe 工具的信息，请参阅 [Stampinf](stampinf.md)。

Inf 项发送 StampInf 任务的参数。 使用项目文件中的 Inf 项可访问 stampinf 的项元数据。

下面的示例演示如何编辑 .vcxproj 文件中的元数据。

```XML
<ItemGroup>
    <Inf Include="a.inf">
      <SpecifyArchitecture>true</SpecifyArchitecture>
      <Architecture>x86</Architecture>
    </Inf>
    <Inf Include="b.inf">
      <SpecifyArchitecture>false</SpecifyArchitecture>
      <Architecture>amd64</Architecture>
    </Inf>
</ItemGroup>
```

下面的示例演示了命令行调用：

```
stampinf.exe –a "x86" a.inf
stampinf.exe b.inf
```

在上面的示例中，MSBuild 同时对 .inf 和 .inf 调用 stampinf.exe，但使用不同的参数集。 对于 b. 即使指定了 **体系结构** 元数据，也会将 **SpecifyArchitecture** 的元数据设置为 false。 因此，在命令行上不启用 **– a** 开关。 如果将此元数据设置为 **TRUE**，则会在命令行上启用 **-amd64** 。 通过这种方式，只需切换此元数据，无需编辑体系结构元数据本身。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">StampInf 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具切换</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>源程序</strong>
<p>必需的 ITaskItem 参数。 指定源文件的列表。</p></td>
<td align="left">% (OutputPath) % (Inf) .inf</td>
<td align="left"><strong>-f</strong><em>[source]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>SpecifyArchitecture</strong>
<p>如果设置为 true，则将启用-a 开关。</p></td>
<td align="left">% (SpecifyArchitecture) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>体系结构</strong>
<p>可选的字符串参数。 指定目标平台体系结构。</p></td>
<td align="left">% (Inf) </td>
<td align="left"><strong>-a</strong><em>[体系结构]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>CatalogFile</strong>
<p>可选的字符串参数。 指定 INF 版本部分中的目录文件指令。</p></td>
<td align="left">% (CatalogFileName) </td>
<td align="left"><strong>-c</strong><em> &lt; catalogFile &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SpecifyDriverVerDirectiveDate</strong>
<p>如果设置为 true，则将启用– d 开关。</p></td>
<td align="left">% (SpecifyDriverVerDirectiveDate) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>DriverVerDirectiveDate</strong>
<p>可选字符串</p></td>
<td align="left">% (日期戳) </td>
<td align="left"><strong>-d</strong> <em>[日期 |<em>]</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>DriverVerDirectiveSection</strong>
<p>可选的字符串参数。 指定应在其中放置 INF DriverVer 指令的 INF 部分。</p></td>
<td align="left">% (DriverVersionSectionName) </td>
<td align="left"><strong>-s</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>SpecifyDriverVerDirectiveVersion</strong>
<p>如果设置为 true，则将启用– v 开关。</p></td>
<td align="left">% (SpecifyDriverDirectiveVersion) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>DriverVerDirectiveVersion</strong>
<p>可选的字符串参数。 指定驱动程序指令中的版本号。</p></td>
<td align="left">% (Inf) </td>
<td align="left"><strong>-v</strong><em>[time |</em>]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>KmdfVersion</strong>
<p>可选的字符串参数。 指定此驱动程序依赖的 KMDF 的版本。</p></td>
<td align="left">% (KmdfVersionNumber) </td>
<td align="left"><strong>-k</strong><em> &lt; 版本 &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>可选的布尔参数。 如果为 true，则执行跟踪的增量生成。 否则，将执行重新生成。</p></td>
<td align="left">% (MinimalRebuildFromTracking) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolPath</strong>
<p>可选的字符串参数。 允许您指定该工具所在的文件夹的完整路径。</p></td>
<td align="left">$ (StampInfToolPath) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>可选的字符串参数。 指定跟踪器用于写入 tlog 的日志目录。</p></td>
<td align="left">% (StampInfTrackerLogDirectory) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackFileAccess</strong>
<p>可选的布尔参数。 如果为 true，则跟踪此任务的文件访问模式。</p></td>
<td align="left">$ (TrackFileAccess) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>UmdfVersion</strong>
<p>可选的字符串参数。 指定此驱动程序依赖的 UMDF 的版本。</p></td>
<td align="left">% (UmdfVersionNumber) </td>
<td align="left"><strong>-u</strong><em> &lt; 版本 &gt; </em></td>
</tr>
<tr class="even">
<td align="left"><strong>程度</strong>
<p>可选的布尔参数。 启用 Stampinf 输出的详细级别。</p></td>
<td align="left">% (EnableVerbose) </td>
<td align="left"><strong>-n</strong></td>
</tr>
</tbody>
</table>

 

 

 





