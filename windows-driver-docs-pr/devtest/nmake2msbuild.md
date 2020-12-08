---
title: Nmake2MsBuild
description: Nmake2MsBuild 实用程序会为驱动程序生成 Visual Studio 项目，该驱动程序是使用您的驱动程序的源代码文件、源、目录和生成文件. inc. 文件中以前版本的 WDK 生成的。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98915de0b11f5f31ee490c7e0dcfb0caba92c0ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828825"
---
# <a name="nmake2msbuild"></a>Nmake2MsBuild


**注意**  从 Windows 10 1511 版开始，从 WDK 中删除了 Nmake2MsBuild 工具。



Nmake2MsBuild 实用程序会为驱动程序生成 Visual Studio 项目，该驱动程序是使用您的驱动程序的源代码文件、 *源*、 *目录* 和 *生成文件. inc.* 文件中以前版本的 WDK 生成的。 实用工具在现有源文件所在的同一目录中创建 Visual Studio *项目文件。* 实用工具不会改变您的源代码或您之前的生成文件。

有关使用此实用工具的信息，请参阅将 [WDK 源文件转换为 Visual Studio 项目](converting-a-wdk-sources-file-to-a-visual-studio-project.md)。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


Nmake2MsBuild.exe 实用工具具有以下语法：

```
NMake2MSBuild.exe  < sources [<sources>...] | dirs >
                          [-Name:<Name of output project>]
                          [-Package:<Path to package project file to generate>]
                          [-Solution:<Path to Solution file to generate>]
                          [-Log:[<LogFile>]:[<Verbosity>]]
                          [-ConsoleLog:<Verbosity>]
                          [-NoPackageProject]
                          [-NoSolution]
                          [-SafeMode]
```

转换工具位于% PROGRAMFILES% \\ Windows 工具包 \\ 8.0 \\ tools \\ x86 \\ directory 目录中。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><em>sources</em></td>
<td align="left"><p>指定使用以前版本的 WDK 构建的驱动程序的 <em>源文件</em> 的路径。 如果 <em>指定源文件，</em> 实用工具将分析 <em>源文件</em> 和相应的 <em>生成</em> 文件，并生成 Visual Studio 项目文件。 Visual Studio 项目文件放置 <em>在源文件所在</em> 的同一目录中。</p>
<p>你可以一次指定多个 <em>源文件</em> 。 所有生成的项目将共享同一个解决方案和包项目。</p></td>
</tr>
<tr class="even">
<td align="left"><em>dirs.proj</em></td>
<td align="left"><p>指定使用以前版本的 WDK 构建的驱动程序的 <em>目录</em> 文件的路径。 如果指定目录文件，实用工具将在目录树中查找所有<em>源文件</em>和对应的生成文件 inc. 文件，并为每<em>个文件生成</em>一个 Visual Studio 项目文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>-Package：</strong>要<em> &lt; 生成 &gt; 的包文件的路径</em></td>
<td align="left">指定驱动程序包项目文件的自定义名称。</td>
</tr>
<tr class="even">
<td align="left"><strong>-解决方案：</strong><em> &lt; 要生成 &gt; 的解决方案文件的路径</em></td>
<td align="left">为驱动程序解决方案文件指定自定义名称 ( .sln) 。</td>
</tr>
<tr class="odd">
<td align="left">-<strong>日志： [</strong><em> &lt; LogFile &gt; </em><strong>]： [</strong><em> &lt; 详细 &gt; 级别</em><strong>]</strong></td>
<td align="left">指定日志文件的名称，并指定日志记录级别 (查看 <em>详细</em> 级别) 。</td>
</tr>
<tr class="even">
<td align="left"><strong>-ConsoleLog：</strong><em> &lt; 详细 &gt; 级别</em></td>
<td align="left">指定控制台日志文件的名称，并指定日志记录级别 (查看 <em>详细</em> 级别) 。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-Name：</strong><em> &lt; 输出项目 &gt; 的名称</em></p></td>
<td align="left"><p>指定将生成的 .Vcxproj 文件的自定义名称。 或者，如果正在转换 <em>目录</em> 文件，则使用此参数指定生成的解决方案的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><em>程度</em></td>
<td align="left">日志文件和控制台日志记录的默认日志记录级别分别为 " <strong>详细</strong> " 和 " <strong>信息</strong> "。 <em>详细级别</em> 是 <strong>SourceLevels</strong>之一。</td>
</tr>
<tr class="odd">
<td align="left"><strong>-安全模式</strong></td>
<td align="left">安全模式不提供对 NMAKE 目标的 IDE/UI 支持，但可以为 NMAKE 目标提供更准确的转换。 仅当在项目的 NMAKE 目标中之前执行的生成步骤过程中遇到问题时，才指定-安全模式。</td>
</tr>
</tbody>
</table>



## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>提出


转换工具位于% PROGRAMFILES% \\ Windows 工具包 \\ 8.0 \\ tools \\ x86 \\ directory 目录中。

响应 (。支持 Rsp) 文件，用于指定命令行参数。 应在单独的行上指定每个参数。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>实例


若要生成使用以前版本的 WDK 构建的驱动程序项目 (使用 Build.exe 和源和目录文件) ，必须首先将其转换为。使用 Nmake2MsBuild.exe 转换实用程序的 .Vcxproj 项目。

例如，若要转换以前使用 Windows 7 WDK （称为 MyDriver）生成的驱动程序，请先打开 **Visual Studio 命令提示符** 窗口。 浏览到目录 *，或者提供* 包含 *源* 或目录生成配置文件的目录的路径。 例如，以下命令将在 *源文件* 所在的文件夹中生成 MyDriver. .vcxproj 文件。

```
nmake2msbuild.exe  .\myDriver\sources
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[将 WDK 源文件转换为 Visual Studio 项目](converting-a-wdk-sources-file-to-a-visual-studio-project.md)

[从现有源文件创建驱动程序](../develop/creating-a-driver-from-existing-source-files.md)
