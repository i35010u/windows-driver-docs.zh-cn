---
title: 消息编译器任务
description: Windows Driver Kit (WDK) 提供 MessageCompiler 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 MC.exe 的工具。 有关使用 MC.exe 的信息，请参阅消息编译器 (MC.exe)。
ms.assetid: 77B2DBF4-64EB-4396-BAA5-80F23C9899CC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ff8bbe41ff03e3392bf439c989ec07b00782cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391337"
---
# <a name="message-compiler-task"></a>消息编译器任务


Windows Driver Kit (WDK) 提供 MessageCompiler 任务，以便在生成您的驱动程序使用 MSBuild 时，可以运行 MC.exe 的工具。 有关使用 MC.exe 的信息，请参阅[**消息编译器 MC.exe**](https://msdn.microsoft.com/library/windows/desktop/aa385638)。

MSBuild 使用 MessageCompile 项发送 MessageCompiler 任务的参数。 MessageCompile 项访问 mc.exe 项目文件中的项元数据。

下面的示例显示了如何编辑.vcxproj 文件中的元数据。

```XML
<ItemGroup>
    <MessageCompile Include="a.mc">
      <GenerateBaselineResource>true</GenerateBaselineResource>
      <BaselineResourcePath>c:\test\</BaselineResourcePath>
    </MessageCompile>
</ItemGroup>
```

下面的示例显示了命令行调用：

```
mc.exe –s "c:\test\" a.mc
```

在上面的示例中，MSBuild 调用 mc.exe 文件 a.mc，使用 – s 开关上的，因为元数据 GenerateBaselineResource 被设置为 true。 此外，MSBuild 使用 BaselineResourcePath 元数据指定 – s 开关的参数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MessageCompiler 任务参数</th>
<th align="left">项元数据</th>
<th align="left">工具开关</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>源</strong>
<p>可选的字符串参数。 指定要编译的清单文件的名称。 指定要编译的消息文件的名称。</p></td>
<td align="left">@(MessageCompile)</td>
<td align="left"><p><strong>&lt;filename.man&gt;</strong></p>
<p><strong>&lt;filename.mc&gt;</strong></p></td>
</tr>
<tr class="even">
<td align="left"><strong>ANSIInputFile</strong>
<p>指定输入文件是 ANSI （默认值）。</p></td>
<td align="left">%(MessageCompile.ANSIInputFile)</td>
<td align="left"><strong>-a</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>ANSIMessageInBinFile</strong>
<p>指定的中的消息。BIN 文件应为 ANSI。</p></td>
<td align="left">%(MessageCompile.ANSIMessageInBinFile)</td>
<td align="left"><strong>-A</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>EnableDebugOutputPath</strong>
<p>如果此值设置为 true，它使 – x 切换。</p></td>
<td align="left">%(MessageCompile.EnableDebugOutputPath)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>DebugOutputPath</strong>
<p>指定编译器将.dbg C 放置到其中的文件夹包含文件。 .Dbg 文件将消息 Id 映射到其符号名称。</p></td>
<td align="left">%(MessageCompile.DebugOutputPath)</td>
<td align="left"><strong>-x</strong><em>&lt;path&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>EnableCallOutMacro</strong>
<p>将添加标注宏，以在日志记录过程中调用用户代码。 此开关不能用于C#将被忽略。</p></td>
<td align="left">%(MessageCompile.EnableCallOutMacro)</td>
<td align="left"><strong>-co</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>EventmanPath</strong>
<p>指定 eventman.xsd 文件的路径。</p></td>
<td align="left">%(MessageCompile.EventmanPath)</td>
<td align="left"><strong>-w</strong><em>&lt;file&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateBaselineResource</strong>
<p>如果此值设置为 true，它使-s 开关。</p></td>
<td align="left">%(MessageCompile.GenerateBaselineResource)</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>BaselineResourcePath</strong>
<p>生成每个提供程序的二进制资源。 生成摘要全局资源 MCGenResource.BIN。</p></td>
<td align="left">%(MessageCompile.BaselineResourcePath)</td>
<td align="left"><strong>-s</strong><em>&lt;path&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateC#LoggingClass</strong>
<p>生成C#（托管） 的日志记录类基于 FX3.5 事件处理类。</p></td>
<td align="left">%(MessageCompile.GenerateC#LoggingClass)</td>
<td align="left"><strong>-cs</strong><em>&lt;namespace&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateC#StaticLoggingClass</strong>
<p>生成静态C#（托管） 的日志记录类基于 FX3.5 事件处理类。</p></td>
<td align="left">%(MessageCompile.GenerateC#StaticLoggingClass)</td>
<td align="left"><strong>-css</strong><em>&lt;namespace&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GeneratedFilesBaseName</strong>
<p>指定生成的文件的基名称。 默认值为输入文件的基名称。</p></td>
<td align="left">%(MessageCompile.GeneratedFilesBaseName)</td>
<td align="left"><strong>-z</strong><em>&lt;basename&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GeneratedHeaderPath</strong>
<p>如果此值设置为 true，它使-h 开关。</p></td>
<td align="left">%(MessageCompile.GeneratedHeaderPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>HeaderFilePath</strong>
<p>指定要在其中创建 C 包含文件的路径。 默认值是...</p></td>
<td align="left">%(MessageCompile.HeaderFilePath)</td>
<td align="left"><strong>-h</strong><em>&lt;path&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GeneratedRcAndMessagesPath</strong>
<p>如果此值设置为 true，它使-r 开关。</p></td>
<td align="left">%(MessageCompile.GeneratedRcAndMessagesPath)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>RCFilePath</strong>
<p>指定的路径的 rc 版包括文件和它包含二进制消息资源文件。 默认值是...</p></td>
<td align="left">%(MessageCompile.RCFilePath)</td>
<td align="left"><strong>-r</strong><em>&lt;path&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateKernelModeLoggingMacros</strong>
<p>生成内核模式日志记录宏。</p></td>
<td align="left">%(MessageCompile.GenerateKernelModeLoggingMacros)</td>
<td align="left"><strong>-km</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateMOFFile</strong>
<p>生成所有函数和宏生成的低级别技术支持。 从清单生成 MOF 文件。 MOF 文件放置在指定的位置"-h"切换。</p></td>
<td align="left">%(MessageCompile.GenerateMOFFile)</td>
<td align="left"><strong>-mof</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateOLE2Header</strong>
<p>生成 OLE2 标头文件。 使用 HRESULT 定义而不是状态代码定义。</p></td>
<td align="left">%(MessageCompile.GenerateOLE2Header)</td>
<td align="left"><strong>-o</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateUserModeLoggingMacros</strong>
<p>生成用户模式下的日志记录宏。</p></td>
<td align="left">%(MessageCompile.GenerateUserModeLoggingMacros)</td>
<td align="left"><strong>-um</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>HeaderExtension</strong>
<p>指定标头文件 （1-3 个字符） 的扩展。</p></td>
<td align="left">%(MessageCompile.HeaderExtension)</td>
<td align="left"><strong>-e</strong><em>&lt;extension&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>MaximumMessageLength</strong>
<p>如果任何消息的大小超过了生成警告&lt;长度&gt;字符。</p></td>
<td align="left">%(MessageCompile.MaximumMessageLength)</td>
<td align="left"><strong>-m</strong><em>&lt;length&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>PrefixMacroName</strong>
<p>定义应用于每个生成的日志记录宏的宏名称前缀。 默认值为"EventWrite"。</p></td>
<td align="left">%(MessageCompile PrefixMacroName)</td>
<td align="left"><strong>-p</strong><em>&lt;prefix&gt;</em></td>
</tr>
<tr class="even">
<td align="left"><strong>RemoveCharsFromSymbolName</strong>
<p>定义宏命名前删除每个事件符号名称开头的文本。 默认值为 NULL。</p></td>
<td align="left">%(RemoveCharsFromSymbolName)</td>
<td align="left"><strong>-P</strong><em>&lt;prefix&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SetCustomerbit</strong>
<p>设置整个消息 ID 中的客户位。</p></td>
<td align="left">%(MessageCompile.SetCustomerbit)</td>
<td align="left"><strong>-c</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>TerminateMessageWithNull</strong>
<p>终止所有字符串包含消息表中的 null 字符。</p></td>
<td align="left">%(MessageCompile.TerminateMessageWithNull)</td>
<td align="left"><strong>-n</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>UnicodeInputFile</strong>
<p>输入的文件是 unicode 格式。</p></td>
<td align="left">%(MessageCompile.UnicodeInputFile)</td>
<td align="left"><strong>-u</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>UnicodeMessageInBinFile</strong>
<p>中的消息。BIN 文件应为 Unicode （默认值）。</p></td>
<td align="left">%(MessageCompile.UnicodeMessageInBinFile)</td>
<td align="left"><strong>-U</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>UseBaseNameOfInput</strong>
<p>指定的。BIN 文件名应具有.mc 文件名包含的唯一性。</p></td>
<td align="left">%(MessageCompile。 UseBaseNameOfInput)</td>
<td align="left"><strong>-b</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>UseDecimalValues</strong>
<p>以十进制表示的标头文件中指定的 FACILTY 和严重性值。 集最初消息标头为十进制表示形式中的值。</p></td>
<td align="left">%(MessageCompile.UseDecimalValues)</td>
<td align="left"><strong>-d</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>ValdateAgainstBaselineResource</strong>
<p>如果此设置为 true，则它会生成-t 开关。</p></td>
<td align="left">%(MessageCompile.ValdateAgainstBaselineResource)</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>BaselinePath</strong>
<p>根据基线资源进行验证。</p></td>
<td align="left">%(MessageCompile.BaselinePath)</td>
<td align="left"><strong>-t</strong><em>&lt;path&gt;</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>Verbose</strong>
<p>指定详细输出。</p></td>
<td align="left">%(MessageCompile.Verbose)</td>
<td align="left"><strong>-v</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>WinmetaPath</strong>
<p>指定 winmeta.xml 文件的路径。</p></td>
<td align="left">%(MessageCompile.WinmetaPath)</td>
<td align="left"><strong>-W</strong><em>&lt;file&gt;</em></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**消息编译器 (MC.exe)**](https://msdn.microsoft.com/library/windows/desktop/aa385638)

 

 






