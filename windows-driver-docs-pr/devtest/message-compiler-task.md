---
title: 消息编译器任务
description: 'Windows 驱动程序工具包 (WDK) 提供 MessageCompiler 任务，以便在使用 MSBuild 构建驱动程序时可以运行 MC.exe 工具。 有关使用 MC.exe 的信息，请参阅 Message 编译器 ( # A1) 。'
ms.assetid: 77B2DBF4-64EB-4396-BAA5-80F23C9899CC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a498019fcd0e4cf1c08df93268ef4ebb5487f69
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384683"
---
# <a name="message-compiler-task"></a>消息编译器任务


Windows 驱动程序工具包 (WDK) 提供 MessageCompiler 任务，以便在使用 MSBuild 构建驱动程序时可以运行 MC.exe 工具。 有关使用 MC.exe 的信息，请参阅 [**Message 编译器 ( # A1) **](/windows/desktop/WES/message-compiler--mc-exe-)。

MSBuild 使用 MessageCompile 项来发送 MessageCompiler 任务的参数。 MessageCompile 项将访问项目文件中 mc.exe 的项元数据。

下面的示例演示如何在 .vcxproj 文件中编辑元数据。

```XML
<ItemGroup>
    <MessageCompile Include="a.mc">
      <GenerateBaselineResource>true</GenerateBaselineResource>
      <BaselineResourcePath>c:\test\</BaselineResourcePath>
    </MessageCompile>
</ItemGroup>
```

下面的示例演示了命令行调用：

```
mc.exe –s "c:\test\" a.mc
```

在上面的示例中，MSBuild 通过– s 开关对文件 a.mc 调用 mc.exe，因为元数据 GenerateBaselineResource 设置为 true。 此外，MSBuild 还使用 BaselineResourcePath 元数据来指定– s 开关的参数。

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
<th align="left">工具切换</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>渠道</strong>
<p>可选的字符串参数。 指定要编译的清单文件的名称。 指定要编译的消息文件的名称。</p></td>
<td align="left">@ (MessageCompile) </td>
<td align="left"><p><strong>&lt;文件名 man&gt;</strong></p>
<p><strong>&lt;filename.mc&gt;</strong></p></td>
</tr>
<tr class="even">
<td align="left"><strong>ANSIInputFile</strong>
<p>指定输入文件为 ANSI (默认) 。</p></td>
<td align="left">% (MessageCompile. ANSIInputFile) </td>
<td align="left"><strong>-a</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>ANSIMessageInBinFile</strong>
<p>指定中的消息。BIN 文件应为 ANSI。</p></td>
<td align="left">% (MessageCompile. ANSIMessageInBinFile) </td>
<td align="left"><strong>-A</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>EnableDebugOutputPath</strong>
<p>如果此值设置为 true，则启用– x 开关。</p></td>
<td align="left">% (MessageCompile. EnableDebugOutputPath) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>DebugOutputPath</strong>
<p>指定编译器在其中放置 dbg C 包含文件的文件夹。 Dbg 文件将消息 Id 映射到其符号名称。</p></td>
<td align="left">% (MessageCompile. DebugOutputPath) </td>
<td align="left"><strong>-x</strong><em> &lt; 路径 &gt; </em></td>
</tr>
<tr class="even">
<td align="left"><strong>EnableCallOutMacro</strong>
<p>添加标注宏，以在日志记录过程中调用用户代码。 此开关对 c # 无效，将被忽略。</p></td>
<td align="left">% (MessageCompile. EnableCallOutMacro) </td>
<td align="left"><strong>-co</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>EventmanPath</strong>
<p>指定 eventman 文件的路径。</p></td>
<td align="left">% (MessageCompile. EventmanPath) </td>
<td align="left"><strong>-w</strong><em> &lt; 文件 &gt; </em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateBaselineResource</strong>
<p>如果此项设置为 true，则启用-s 开关。</p></td>
<td align="left">% (MessageCompile. GenerateBaselineResource) </td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>BaselineResourcePath</strong>
<p>为每个提供程序生成二进制资源。 生成摘要全局资源 MCGenResource。</p></td>
<td align="left">% (MessageCompile. BaselineResourcePath) </td>
<td align="left"><strong>-s</strong><em> &lt; 路径 &gt; </em></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateC#LoggingClass</strong>
<p>基于 FX 3.5 事件类生成 c # (托管) 日志记录类。</p></td>
<td align="left">% (MessageCompile. GenerateC # LoggingClass) </td>
<td align="left"><strong>-cs</strong><em> &lt; 命名 &gt; 空间</em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateC#StaticLoggingClass</strong>
<p>基于 FX 3.5 事件类，生成静态 c # (托管) 日志记录类。</p></td>
<td align="left">% (MessageCompile. GenerateC # StaticLoggingClass) </td>
<td align="left"><strong>-css</strong><em> &lt; 命名 &gt; 空间</em></td>
</tr>
<tr class="even">
<td align="left"><strong>GeneratedFilesBaseName</strong>
<p>指定生成的文件的基名称。 默认值为输入文件的 basename。</p></td>
<td align="left">% (MessageCompile. GeneratedFilesBaseName) </td>
<td align="left"><strong>-z</strong><em> &lt; basename &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GeneratedHeaderPath</strong>
<p>如果此项设置为 true，则启用-h 开关。</p></td>
<td align="left">% (MessageCompile. GeneratedHeaderPath) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>HeaderFilePath</strong>
<p>指定创建 C 包含文件的位置的路径。 默认值为.。</p></td>
<td align="left">% (MessageCompile. HeaderFilePath) </td>
<td align="left"><strong>-h</strong><em> &lt; 路径 &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GeneratedRcAndMessagesPath</strong>
<p>如果此项设置为 true，则启用-r 开关。</p></td>
<td align="left">% (MessageCompile. GeneratedRcAndMessagesPath) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>RCFilePath</strong>
<p>指定 RC 的路径包含文件以及它包含的二进制消息资源文件。 默认值为.。</p></td>
<td align="left">% (MessageCompile. RCFilePath) </td>
<td align="left"><strong>-r</strong><em> &lt; 路径 &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateKernelModeLoggingMacros</strong>
<p>生成内核模式日志记录宏。</p></td>
<td align="left">% (MessageCompile. GenerateKernelModeLoggingMacros) </td>
<td align="left"><strong>-公里</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateMOFFile</strong>
<p>为生成的所有函数和宏生成下级支持。 MOF 文件是从清单生成的。 MOF 文件放置在 "-h" 开关指定的位置。</p></td>
<td align="left">% (MessageCompile. GenerateMOFFile) </td>
<td align="left"><strong>-mof</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>GenerateOLE2Header</strong>
<p>生成 OLE2 头文件。 使用 HRESULT 定义，而不是状态代码定义。</p></td>
<td align="left">% (MessageCompile. GenerateOLE2Header) </td>
<td align="left"><strong>-o</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>GenerateUserModeLoggingMacros</strong>
<p>生成用户模式日志记录宏。</p></td>
<td align="left">% (MessageCompile. GenerateUserModeLoggingMacros) </td>
<td align="left"><strong>-um</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>HeaderExtension</strong>
<p>指定标头文件的扩展 (1-3 个字符) 。</p></td>
<td align="left">% (MessageCompile. HeaderExtension) </td>
<td align="left"><strong>-e</strong><em> &lt; 扩展 &gt; </em></td>
</tr>
<tr class="even">
<td align="left"><strong>MaximumMessageLength</strong>
<p>如果任何消息的大小超过长度字符，则生成警告 &lt; &gt; 。</p></td>
<td align="left">% (MessageCompile. MaximumMessageLength) </td>
<td align="left"><strong>-m</strong><em> &lt; 长度 &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>PrefixMacroName</strong>
<p>定义应用于每个生成的日志记录宏的宏名称前缀。 默认值为 "EventWrite"。</p></td>
<td align="left">% (MessageCompile PrefixMacroName) </td>
<td align="left"><strong>-p</strong><em> &lt; 前缀 &gt; </em></td>
</tr>
<tr class="even">
<td align="left"><strong>RemoveCharsFromSymbolName</strong>
<p>在形成宏名之前，定义要删除的每个事件符号名称开头的文本。 默认值为 NULL。</p></td>
<td align="left">% (RemoveCharsFromSymbolName) </td>
<td align="left"><strong>-P</strong><em> &lt; 前缀 &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>SetCustomerbit</strong>
<p>在整个消息 ID 中设置客户位。</p></td>
<td align="left">% (MessageCompile. SetCustomerbit) </td>
<td align="left"><strong>-c</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>TerminateMessageWithNull</strong>
<p>终止消息表中所有包含空字符的字符串。</p></td>
<td align="left">% (MessageCompile. TerminateMessageWithNull) </td>
<td align="left"><strong>-n</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>UnicodeInputFile</strong>
<p>输入文件是 Unicode。</p></td>
<td align="left">% (MessageCompile. UnicodeInputFile) </td>
<td align="left"><strong>-u</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>UnicodeMessageInBinFile</strong>
<p>消息。BIN 文件应为 Unicode (默认) 。</p></td>
<td align="left">% (MessageCompile. UnicodeMessageInBinFile) </td>
<td align="left"><strong>-U</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>UseBaseNameOfInput</strong>
<p>指定。为实现唯一性，BIN 文件名应包含 mc 文件名。</p></td>
<td align="left"> (MessageCompile。 UseBaseNameOfInput) </td>
<td align="left"><strong>-b</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>UseDecimalValues</strong>
<p>指定标头文件中的 FACILTY 和严重性值（十进制）。 最初将标头中的消息值设置为十进制。</p></td>
<td align="left">% (MessageCompile. UseDecimalValues) </td>
<td align="left"><strong>-d</strong></td>
</tr>
<tr class="odd">
<td align="left"><strong>ValdateAgainstBaselineResource</strong>
<p>如果此值设置为 true，则生成-t 开关。</p></td>
<td align="left">% (MessageCompile. ValdateAgainstBaselineResource) </td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>BaselinePath</strong>
<p>根据基线资源进行验证。</p></td>
<td align="left">% (MessageCompile. BaselinePath) </td>
<td align="left"><strong>-t</strong><em> &lt; 路径 &gt; </em></td>
</tr>
<tr class="odd">
<td align="left"><strong>详细</strong>
<p>指定详细输出。</p></td>
<td align="left">% (MessageCompile) </td>
<td align="left"><strong>-v</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>WinmetaPath</strong>
<p>指定 winmeta.xml 文件的路径。</p></td>
<td align="left">% (MessageCompile. WinmetaPath) </td>
<td align="left"><strong>-W</strong><em> &lt; 文件 &gt; </em></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**消息编译器 (MC.exe)**](/windows/desktop/WES/message-compiler--mc-exe-)

 

