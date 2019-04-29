---
title: Nmake2MsBuild
description: Nmake2MsBuild 实用程序生成的驱动程序，使用以前版本的 WDK 驱动程序的源代码文件中，从和源、 目录和 makefile.inc 文件生成的 Visual Studio 项目。
ms.assetid: D6E1C124-9A5F-486B-865E-45A0BC58A5A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b896b9147b2e5470c27992cad01a6fd1d766952
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374655"
---
# <a name="nmake2msbuild"></a>Nmake2MsBuild


**请注意**Nmake2MsBuild 工具已从 WDK 从 Windows 10，版本 1511年开始。



Nmake2MsBuild 实用程序生成的驱动程序，使用以前版本的 WDK 从驱动程序的源代码文件，并从生成的 Visual Studio 项目*源*，*目录*，和*makefile.inc*文件。 该实用程序与现有的相同目录中创建 Visual Studio 项目文件*源*文件。 该实用工具不会更改你的源代码或更早的生成文件。

有关使用该实用工具的信息，请参阅[转换 WDK 源到 Visual Studio 项目文件](converting-a-wdk-sources-file-to-a-visual-studio-project.md)。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>语法


Nmake2MsBuild.exe 实用程序具有以下语法：

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

转换工具位于 %PROGRAMFILES%\\Windows 工具包\\8.0\\工具\\x86\\目录。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><em>sources</em></td>
<td align="left"><p>指定的路径<em>源</em>驱动程序使用以前版本的 WDK 构建的文件。 如果指定<em>源</em>文件，该实用工具将它解析<em>源</em>文件和相应<em>makefile.inc</em>并生成 Visual Studio 项目文件。 Visual Studio 项目文件所在的同一目录中放置<em>源</em>文件。</p>
<p>您可以指定多个<em>源</em>文件一次。 生成的所有项目将都共享相同的解决方案和包项目。</p></td>
</tr>
<tr class="even">
<td align="left"><em>dirs</em></td>
<td align="left"><p>指定的路径<em>目录</em>驱动程序使用以前版本的 WDK 构建的文件。 如果指定<em>目录</em>文件，该实用程序看起来在目录树中的所有<em>源</em>文件和相应 makefile.inc 文件并生成每个 Visual Studio 项目文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>包：</strong><em>&lt;包文件的路径来生成&gt;</em></td>
<td align="left">指定驱动程序包项目文件的自定义名称。</td>
</tr>
<tr class="even">
<td align="left"><strong>解决方案：</strong><em>&lt;生成解决方案文件路径&gt;</em></td>
<td align="left">指定驱动程序的解决方案文件 (.sln) 的自定义名称。</td>
</tr>
<tr class="odd">
<td align="left">-<strong>Log:[</strong><em>&lt;LogFile&gt;</em><strong>]:[</strong><em>&lt;Verbosity&gt;</em><strong>]</strong></td>
<td align="left">指定日志文件的名称和指定的日志记录级别 (请参阅<em>详细级别</em>)。</td>
</tr>
<tr class="even">
<td align="left"><strong>-ConsoleLog:</strong><em>&lt;详细级别&gt;</em></td>
<td align="left">指定控制台日志文件的名称和指定的日志记录级别 (请参阅<em>详细级别</em>)。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>名称：</strong><em>&lt;输出项目的名称&gt;</em></p></td>
<td align="left"><p>指定将生成的 VcxProj 文件的自定义名称。 或者，如果<em>目录</em>正在转换文件，此参数用于指定生成的解决方案的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><em>详细级别</em></td>
<td align="left">默认日志记录级别的日志文件和控制台日志记录<strong>Verbose</strong>并<strong>信息</strong>分别。 <em>详细程度</em>是之一<strong>System.Diagnostics.SourceLevels</strong>。</td>
</tr>
<tr class="odd">
<td align="left"><strong>-SafeMode</strong></td>
<td align="left">安全模式的 NMAKE 目标，不提供 IDE/UI 支持，但可以提供更准确地转换为 NMAKE 目标。 如果在项目的 NMAKE 目标中之前执行的生成步骤过程中出现问题，请仅指定-安全模式。</td>
</tr>
</tbody>
</table>



## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>注释


转换工具位于 %PROGRAMFILES%\\Windows 工具包\\8.0\\工具\\x86\\目录。

响应 (。用于指定命令行参数支持 Rsp) 文件。 应在单独的行上指定每个参数。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


若要生成已生成与以前版本的 WDK （使用 Build.exe 和源和目录文件） 的驱动程序项目，您必须首先将其转换为。VcxProj 使用 Nmake2MsBuild.exe 转换实用工具项目。

例如，要转换的驱动程序，以前使用 Windows 7 WDK，名为 MyDriver，生成首次打开**Visual Studio 命令提示符**窗口。 浏览到目录或提供包含的目录的路径*源*或*目录*生成配置文件。 例如，下面的命令相同的文件夹中生成 MyDriver.Vcxproj 文件*源*文件。

```
nmake2msbuild.exe  .\myDriver\sources
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[将 WDK 源文件转换为 Visual Studio 项目](converting-a-wdk-sources-file-to-a-visual-studio-project.md)

[从现有源文件创建驱动程序](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_from_existing_source_files)










