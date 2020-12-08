---
title: Ctrpp 任务
description: Windows 驱动程序工具包 (WDK) 提供 Ctrpp 任务，以便在使用 MSBuild 构建驱动程序时可以运行 ctrpp.exe 工具。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9858fb9ddec1d81ed68e1c49a055b3118199fa2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832821"
---
# <a name="ctrpp-task"></a>Ctrpp 任务


Windows 驱动程序工具包 (WDK) 提供 Ctrpp 任务，以便在使用 MSBuild 构建驱动程序时可以运行 ctrpp.exe 工具。 有关使用 ctrpp.exe 的信息，请参阅 [**CTRPP**](/windows/desktop/PerfCtrs/ctrpp)。

MSBuild 使用 Ctrpp 项将 Ctrpp 任务的参数发送到 ctrpp.exe。 项目文件中的 Ctrpp 项访问 ctrpp.exe 的项元数据。

下面的示例演示如何在 .vcxproj 文件中编辑元数据。

```XML
<ItemGroup>
    <Ctrpp Include="a.manifest">
      <GenerateHeaderFileForCounter>true</GenerateHeaderFileForCounter>
      <HeaderFileNameForCounter>c:\test\abc.h</HeaderFileNameForCounter>
    </Ctrpp>
</ItemGroup>
```

下面的示例演示了命令行调用：

```
ctrpp.exe –ch "c:\test\abc.h" a.manifest
```

在上面的示例中，MSBuild 使用 **– ch** 选项调用文件 GenerateHeaderFileForCounter 上的 ctrpp.exe，因为元数据的设置为 true。 此外，MSBuild 使用 HeaderFileNameForCounter 元数据指定 **– ch** 选项的参数

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Ctrpp 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具切换</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Source</td>
<td align="left">@ (Ctrpp) </td>
<td align="left"></td>
<td align="left">必需的 ITaskItem 参数。 指定要处理的计数器清单。</td>
</tr>
<tr class="even">
<td align="left">AddPrefix</td>
<td align="left">% (Ctrpp. AddPrefix) </td>
<td align="left"><strong>-前缀</strong><em> &lt; 前缀 &gt; </em></td>
<td align="left">可选的字符串参数。 指定要添加到生成的函数和变量的前缀。</td>
</tr>
<tr class="odd">
<td align="left">BackwardCompatibility</td>
<td align="left">% (Ctrpp. BackwardCompatibility) </td>
<td align="left"><strong>-backcompat</strong></td>
<td align="left">可选的布尔参数。 生成与 Windows 7 之前的操作系统二进制兼容的代码。</td>
</tr>
<tr class="even">
<td align="left">EnableLegacy</td>
<td align="left">% (Ctrpp. EnableLegacy) </td>
<td align="left"><strong>-旧版</strong></td>
<td align="left">可选的布尔参数。 恢复到以前的 ctrpp 文件。 此开关会导致 ctrpp 生成四个输出文件：两个标头文件、一个资源文件和一个源代码文件。 这模拟了 ctrpp 以前版本中的行为。 -O、-ch、-rc 和-prefix 选项不能与-legacy 一起使用。</td>
</tr>
<tr class="odd">
<td align="left">GeneratedCounterFilesPath</td>
<td align="left">% (Ctrpp. GeneratedCounterFilesPath) </td>
<td align="left"><strong>-sumPath</strong><em> &lt; 路径 &gt; </em></td>
<td align="left">可选的字符串参数。 指定用于生成二进制计数器文件的路径（默认值）。</td>
</tr>
<tr class="even">
<td align="left">GenerateHeaderFileForCounter</td>
<td align="left">% (Ctrpp. GenerateHeaderFileForCounter) </td>
<td align="left"></td>
<td align="left">如果此项设置为 true，则启用-ch 开关。</td>
</tr>
<tr class="odd">
<td align="left">HeaderFileNameForCounter</td>
<td align="left">% (Ctrpp. HeaderFileNameForCounter) </td>
<td align="left"><strong>-ch</strong><em> &lt; filename &gt; </em></td>
<td align="left">可选的字符串参数。 生成包含计数器名称和 id 的标头文件。</td>
</tr>
<tr class="even">
<td align="left">GenerateHeaderFileForProvider</td>
<td align="left">% (Ctrpp. GenerateHeaderFileForProvider) </td>
<td align="left"></td>
<td align="left">如果此值设置为 true，则启用-o 开关。</td>
</tr>
<tr class="odd">
<td align="left">HeaderFileNameForProvider</td>
<td align="left">% (Ctrpp. HeaderFileNameForProvider) </td>
<td align="left"><strong>-o</strong><em> &lt; filename &gt; </em></td>
<td align="left">可选的字符串参数。 为提供程序生成标头文件。</td>
</tr>
<tr class="even">
<td align="left">GenerateMemoryRoutines</td>
<td align="left">% (Ctrpp. GenerateMemoryRoutines) </td>
<td align="left"><strong>-MemoryRoutines</strong></td>
<td align="left">可选的布尔参数。 生成内存分配和免费例程模板。</td>
</tr>
<tr class="odd">
<td align="left">GenerateNotificationCallback</td>
<td align="left">% (Ctrpp. GenerateNotificationCallback) </td>
<td align="left"><strong>-NotificationCallback</strong></td>
<td align="left">可选的布尔参数。 生成自定义的通知回调模板。 类似于 provider 元素中的 "callback" &lt; 特性 &gt; 。</td>
</tr>
<tr class="even">
<td align="left">GenerateResourceSourceFile</td>
<td align="left">% (Ctrpp. GenerateResourceSourceFile) </td>
<td align="left"></td>
<td align="left">如果此值设置为 true，则启用-rc 开关。</td>
</tr>
<tr class="odd">
<td align="left">ResourceFileName</td>
<td align="left">% (Ctrpp. ResourceFileName) </td>
<td align="left"><strong>-rc</strong><em> &lt; filename &gt; </em></td>
<td align="left">可选的字符串参数。 生成资源源文件。</td>
</tr>
<tr class="even">
<td align="left">GenerateSummaryGlobalFile</td>
<td align="left">% (Ctrpp. GeneratedSummaryGlobalFile) </td>
<td align="left"><strong>-摘要</strong><em> &lt; 路径 &gt; </em></td>
<td align="left">可选的字符串参数。 为每个提供程序生成二进制计数器文件生成摘要全局文件 GenSumResource。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**CTRPP**](/windows/desktop/PerfCtrs/ctrpp)
