---
title: Stampinf 任务
description: Windows Driver Kit (WDK) 提供 StampInf 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 stampinf.exe 工具。 有关 stampinf.exe 工具的信息，请参阅 Stampinf。
ms.assetid: 4BD937D3-97C7-408D-9372-F01CBB7B0B62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10c3bd71fcf98d267647c0c42f8012f94bdc949d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543225"
---
# <a name="stampinf-task"></a>Stampinf 任务


Windows Driver Kit (WDK) 提供 StampInf 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 stampinf.exe 工具。 有关 stampinf.exe 工具的信息，请参阅[Stampinf](stampinf.md)。

Inf 项发送 StampInf 任务的参数。 在项目文件中使用 Inf 项访问 stampinf 的项元数据。

下面的示例演示如何在.vcxproj 文件中的编辑元数据。

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

下面的示例显示了命令行调用：

```
stampinf.exe –a "x86" a.inf
stampinf.exe b.inf
```

在上面的示例中，MSBuild 调用 stampinf.exe a.inf 和 b.inf，但具有不同的参数集。 对于 b.inf，即使**体系结构**指定的元数据，则**SpecifyArchitecture**元数据设置为 false。 因此， **– a**交换机未启用命令行上。 如果此元数据设置为 **，则返回 TRUE**，然后将启用 **– a amd64**命令行上。 这样一来，可以只需切换此元数据，而无需编辑体系结构元数据本身。

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
<th align="left">工具开关</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>源</strong>
<p>所需的 ITaskItem 参数。 指定源文件的列表。</p></td>
<td align="left">%(Inf.OutputPath)%(Inf.FileName).inf</td>
<td align="left"><strong>-f</strong><em>[source]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>SpecifyArchitecture</strong>
<p>如果将启用-a 开关设置为 true。</p></td>
<td align="left">%(Inf.SpecifyArchitecture)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>体系结构</strong>
<p>可选的字符串参数。 指定目标平台体系结构。</p></td>
<td align="left">%(Inf.Architecture)</td>
<td align="left"><strong>-a</strong><em>[architecture]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>CatalogFile</strong>
<p>可选的字符串参数。 INF 版本部分中指定的目录文件指令。</p></td>
<td align="left">%(Inf.CatalogFileName)</td>
<td align="left"><strong>-c</strong><em>&lt;catalogFile&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SpecifyDriverVerDirectiveDate</strong>
<p>这将使 – d 开关，如果设置为 true。</p></td>
<td align="left">%(Inf.SpecifyDriverVerDirectiveDate)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>DriverVerDirectiveDate</strong>
<p>可选的字符串</p></td>
<td align="left">%(Inf.DateStamp)</td>
<td align="left"><strong>-d</strong><em>[date|<em>]</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>DriverVerDirectiveSection</strong>
<p>可选的字符串参数。 指定应在其中放置 INF DriverVer 指令的 INF 部分。</p></td>
<td align="left">%(Inf.DriverVersionSectionName)</td>
<td align="left"><strong>-s</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>SpecifyDriverVerDirectiveVersion</strong>
<p>这将使 – v 开关，如果设置为 true。</p></td>
<td align="left">%(Inf.SpecifyDriverDirectiveVersion)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>DriverVerDirectiveVersion</strong>
<p>可选的字符串参数。 驱动程序指令中指定的版本号。</p></td>
<td align="left">%(Inf.TimeStamp)</td>
<td align="left"><strong>-v</strong><em>[time|</em>]</em></td>
</tr>
<tr class="even">
<td align="left"><strong>KmdfVersion</strong>
<p>可选的字符串参数。 指定此驱动程序依赖的 KMDF 的版本。</p></td>
<td align="left">%(Inf.KmdfVersionNumber)</td>
<td align="left"><strong>-k</strong><em>&lt;version&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>MinimalRebuildFromTracking</strong>
<p>可选布尔参数。 如果为 true，则执行跟踪的增量生成。 否则，执行重新生成。</p></td>
<td align="left">%(Inf.MinimalRebuildFromTracking)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>ToolPath</strong>
<p>可选的字符串参数。 可以指定该工具所在的文件夹的完整路径。</p></td>
<td align="left">$(StampInfToolPath)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TrackerLogDirectory</strong>
<p>可选的字符串参数。 指定跟踪器编写 tlog 的日志目录。</p></td>
<td align="left">%(Inf.StampInfTrackerLogDirectory)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TrackFileAccess</strong>
<p>可选布尔参数。 如果为 true，则跟踪文件访问模式，此任务。</p></td>
<td align="left">$(TrackFileAccess)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>UmdfVersion</strong>
<p>可选的字符串参数。 指定 UMDF 取决于此驱动程序版本。</p></td>
<td align="left">%(Inf.UmdfVersionNumber)</td>
<td align="left"><strong>-u</strong><em>&lt;version&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>详细级别</strong>
<p>可选布尔参数。 使 Stampinf 输出的详细级别。</p></td>
<td align="left">%(Inf.EnableVerbose)</td>
<td align="left"><strong>-n</strong></td>
</tr>
</tbody>
</table>

 

 

 





