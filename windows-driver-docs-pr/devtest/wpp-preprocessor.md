---
title: WPP 预处理器
description: WPP 预处理器
ms.assetid: 92bcb2c4-f6de-4704-8f5c-9a2e5901616a
keywords:
- Windows 软件跟踪预处理器 WDK，选项
- WPP 软件跟踪 WDK，选项
- WPP 预处理器 WDK
- Windows 软件跟踪预处理器 WDK，调用预处理器
- WPP 软件跟踪 WDK，调用预处理器
- Windows 软件跟踪预处理器 WDK，生成过程
- WPP 软件跟踪 WDK，生成过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e672ac1ed5bbde2aafe0e95969e40eba8535e669
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382165"
---
# <a name="wpp-preprocessor"></a>WPP 预处理器


本部分介绍 *Windows 软件跟踪预处理器*，通常称为 WPP 预处理器。

## <a name="span-idinvoking_the_wpp_preprocessorspanspan-idinvoking_the_wpp_preprocessorspan-invoking-the-wpp-preprocessor"></a><span id="invoking_the_wpp_preprocessor"></span><span id="INVOKING_THE_WPP_PREPROCESSOR"></span> 调用 WPP 预处理器


可以使用 Visual Studio 和 MSBuild 环境调用 WPP 预处理器。

**调用 WPP 预处理器**

1.  在解决方案资源管理器中右键单击驱动程序项目，然后单击 " **属性"。**
2.  在项目属性页中，单击 "**配置属性**"，然后单击 " **WPP 跟踪**"
3.  在 " **常规**" 下，将 " **运行 WPP** " 选项设置为 **"是"**。
4.  在 " **命令行**" 下，你可以添加下面的选项来自定义跟踪行为。

    例如，在 **WPP 跟踪**下，可以指定单个 **扫描配置数据** 文件。

    如果需要提供多个配置文件，例如，要指定自定义数据类型，请使用 **-scan**选项在**命令行**中引用该文件，例如：

    ```
    -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\WdfTraceEnums.h"
    ```

有关生成过程的详细信息，请参阅 [TraceWPP 任务](tracewpp-task.md) 和 [WDK 和 Visual Studio 生成环境](wdk-and-visual-studio-build-environment.md)。

你还可以通过使用 TraceWPP 工具 ( # A0) ，从生成环境中单独运行预处理器。 此工具位于 WDK 的 bin/x86 子目录中。

## <a name="span-idwpp_tracing_general_optionsspanspan-idwpp_tracing_general_optionsspanspan-idwpp_tracing_general_optionsspanwpp-tracing-general-options"></a><span id="WPP_Tracing_General_Options"></span><span id="wpp_tracing_general_options"></span><span id="WPP_TRACING_GENERAL_OPTIONS"></span>WPP 跟踪常规选项


下表描述了 WPP 预处理器的选项。 你可以在 Visual Studio 中使用项目的 WPP 跟踪属性页或 TraceWPP 工具的参数来配置这些选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 跟踪选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 WPP</p></td>
<td align="left"><p>如果为 true，则调用 WPP。</p></td>
</tr>
<tr class="even">
<td align="left"><p>启用最小重新生成</p></td>
<td align="left"><p>如果为 true，则执行跟踪的增量生成;如果为 false，则执行重新生成。</p></td>
</tr>
</tbody>
</table>

 

## <span id="run_wpp_options"></span><span id="RUN_WPP_OPTIONS"></span>


## <a name="span-idfunction_and_macro_optionsspanspan-idfunction_and_macro_optionsspanspan-idfunction_and_macro_optionsspanfunction-and-macro-options"></a><span id="Function_and_Macro_Options"></span><span id="function_and_macro_options"></span><span id="FUNCTION_AND_MACRO_OPTIONS"></span>函数和宏选项


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 跟踪选项</th>
<th align="left">TraceWPP 命令选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>预处理器定义</p></td>
<td align="left"><p><strong>-D</strong><em>宏</em></p></td>
<td align="left"><p>将<strong> # define</strong> <em>宏</em>添加到生成的文件的开头，其中<em>宏命令</em>为宏的名称。</p>
<p>此选项与 <strong>/d</strong> (定义宏) 编译器选项相同。 包含此方法是为了确保定义在 TMH 文件的开头有效。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p><strong>-D</strong><em>宏</em> <strong>=</strong> <em>展开</em></p></td>
<td align="left"><p>将 " <strong> # 定义</strong><em>宏展开</em>" 添加到生成的文件的开头，其中<em>宏命令</em>为宏的名称，<em>展开为展开</em>值。</p>
<p>此选项与 <strong>/d</strong> (定义宏) 编译器选项相同。 包含此方法是为了确保定义在 TMH 文件的开头有效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>跟踪内核模式组件</p></td>
<td align="left"><p><strong>-公里</strong></p></td>
<td align="left"><p>定义跟踪内核模式组件的 WPP_KERNEL_MODE 宏。 默认情况下，只跟踪用户模式组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>启用 Dll 宏</p></td>
<td align="left"><p><strong>-dll</strong></p></td>
<td align="left"><p>定义 WPP_DLL 宏，该宏会在调用 WPP_INIT_TRACING 时初始化 WPP 数据结构。 否则，结构只会初始化一次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>指定控件 GUID</p></td>
<td align="left"><p><strong>-ctl：</strong> <em>GUID</em></p></td>
<td align="left">定义一个 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)" data-raw-source="[WPP_CONTROL_GUIDS](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))">WPP_CONTROL_GUIDS</a> 宏，其中包含指定的 <a href="control-guid.md" data-raw-source="[control GUID](control-guid.md)">控件 GUID</a> 和名为 "错误"、"异常" 和 "干扰" 的 WPP_DEFINE_BIT 条目。
<p>这是将宏添加到源文件中的替代方法。</p>
<p><em>Guid</em> 表示控件 guid。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsearch_and_formatting_optionsspanspan-idsearch_and_formatting_optionsspanspan-idsearch_and_formatting_optionsspansearch-and-formatting-options"></a><span id="Search_and_Formatting_Options"></span><span id="search_and_formatting_options"></span><span id="SEARCH_AND_FORMATTING_OPTIONS"></span>搜索和格式设置选项


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 跟踪选项</th>
<th align="left">TraceWPP 命令选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>忽略感叹号</p></td>
<td align="left"><p><strong>-noshrieks</strong></p></td>
<td align="left"><p>指示 WPP 忽略感叹号，也称为 "shrieks"。</p>
<p>用于复杂格式，如%！ timestamp！%。 默认情况下，惊叹号是必需的，而 WPP 尝试解释它们。</p></td>
</tr>
<tr class="even">
<td align="left"><p>格式字符串的数字基数</p></td>
<td align="left"><p><strong>-argbase：</strong> <em>Number</em></p></td>
<td align="left"><p>为格式字符串（如 "%1！ d！，%2！ s！"）建立数字基数。 默认值为 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>用于生成跟踪消息的函数</p></td>
<td align="left"><p><strong>-func：</strong> <em>FunctionDescription</em></p></td>
<td align="left"><p>指定 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"><strong>DoTraceMessage</strong></a> 宏的替代项。 然后，可以使用这些函数来生成跟踪消息。</p>
<p>例如，可以定义一个函数，该函数同时指定跟踪消息的标志和级别，例如：</p>
<pre space="preserve"><code>-func (DoMyTraceMessage(LEVEL,FLAGS,MSG,...)</code></pre>
<p>可以使用 <strong>-func</strong> 选项的多个实例。</p>
<p>此选项是在本地配置文件中指定函数说明的替代方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p>指定要搜索的字符串</p></td>
<td align="left"><p><strong>-lookfor：</strong><em>String</em></p></td>
<td align="left"><p>指示 WPP 搜索指定字符串的源文件以启动跟踪。 默认情况下，WPP 会搜索字符串 "WPP_INIT_TRACING"。</p>
<p>这是一个高级选项，适用于正在编写自己的模板的用户。</p>
<p>例如，在默认情况下，tpl：</p>
<pre space="preserve"><code><code>IF FOUND WPP_INIT_TRACING</code>
 <code>INCLUDE um-init.tpl</code>
<code>ENDIF</code></code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p>指定模块名称</p></td>
<td align="left"><p><strong>-p：</strong> <em>String</em></p></td>
<td align="left"><p>指定此<a href="trace-provider.md" data-raw-source="[trace provider](trace-provider.md)">跟踪提供程序</a>中消息的<a href="message-guid.md" data-raw-source="[message GUID](message-guid.md)">消息 GUID</a>的备用友好名称。 默认情况下，消息 GUID 的友好名称是在其中生成跟踪提供程序的目录的名称。</p>
<p>默认情况下，消息 GUID 的友好名称显示在由变量 " <strong>%1</strong>" 表示的<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">跟踪消息前缀</a>中。 你可以使用此参数将一个字符串添加到前缀，该前缀可帮助用户标识跟踪提供程序，例如跟踪提供程序的友好名称、包含跟踪提供程序的模块的名称或通过创建多个跟踪提供程序实现的项目的名称。 此信息可帮助用户关联不同文件中的相关跟踪提供程序或不同的路径。</p>
<p><strong>-P</strong>参数需要适用于 windows Vista 和更高版本的 Wdk 的 Windows 驱动程序工具包 (wdk) 中包含的 WPP 版本。 <strong>-P</strong>参数适用于 windows 2000 和更高版本的 windows。</p>
<p>示例：</p>
<pre space="preserve"><code>-p:TraceDrv
-p:AudioModule</code></pre></td>
</tr>
</tbody>
</table>

 

## <a name="span-idfile_optionsspanspan-idfile_optionsspanspan-idfile_optionsspanfile-options"></a><span id="File_Options"></span><span id="file_options"></span><span id="FILE_OPTIONS"></span>文件选项


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 跟踪选项</th>
<th align="left">TraceWPP 命令选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>附加包含目录</p></td>
<td align="left"><p><strong>-I</strong> <em>Path1</em><strong>[;</strong><em>Path2</em><strong>]</strong></p></td>
<td align="left"><p>指定一个或多个要添加到包含路径中的目录；存在多个目录时，请用分号分隔。 与-<strong>cfgdir</strong>相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p>配置目录</p></td>
<td align="left"><p><strong>-cfgdir：</strong> <em>Path1</em><strong>[;</strong><em>Path2</em><strong>]</strong></p></td>
<td align="left"><p>指定配置文件和模板文件的位置。</p>
<p><em>Path1</em> 和 <em>Path2</em> 表示目录的完全限定路径。 可以指定多个路径。 默认值为本地目录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>文件扩展名</p></td>
<td align="left"><p><strong>-ext：。</strong> <em>ext1</em> <strong>[。</strong><em>ext2</em><strong>]</strong></p></td>
<td align="left"><p>指定 WPP 识别为源文件的文件类型。 WPP 将忽略具有不同文件扩展名的文件。</p>
<p>默认情况下，WPP 仅识别 .c、c + +、.cpp 和 .cxx 文件。</p>
<p>使用此选项，可以使用 WPP 的默认设置，而无需删除或重命名 WPP 不使用的资源文件（如 .rc 和 mc 文件）。</p>
<p>例如，若要将跟踪添加到 c + + 文件和标头 () 文件，请使用以下命令：</p>
<p><strong>-ext： .cpp。CPP。h</strong></p>
<p>此外，若要为 c + + 文件和头文件提供不同名称的 TMH 文件，请使用 <strong>-preserveext</strong> 选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>保留文件扩展名</p></td>
<td align="left"><p><strong>-preserveext：</strong> <em>. ext1</em><strong>[。</strong><em>ext2</em><strong>]</strong></p></td>
<td align="left"><p>创建 TMH 文件时，保留指定的文件扩展名。</p>
<p>默认情况下，所有文件类型的 TMH 文件都<em>命名为 TMH。</em> 如果有多个同名的源文件，这将导致文件名冲突。</p>
<p>例如，默认情况下， ( C 文件的 TMH 文件) 和标头 ( .h) 文件将命名为 &lt; &gt; TMH。 通过使用 <strong>-preserveext： .c .h</strong>，TMH 文件的名称为 &lt; &gt; TMH 和和 &lt; &gt; TMH。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>输出目录</p></td>
<td align="left"><strong>-odir：</strong> <em>path</em></td>
<td align="left"><p>指定 WPP 创建的输出文件的目录。</p>
<p><em>路径</em> 是目录的完全限定路径。 默认值为本地目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p>指定模板文件</p></td>
<td align="left"><p><strong>-gen { <em> File。 宋体</strong></p></td>
<td align="left"><p>对于具有在大括号之间指定的名称进行 WPP 处理的每个源文件 {} ，请创建另一个具有指定文件扩展名的文件。</p>
<p>文件 tpl 表示源文件。 * ext 表示创建的文件类型及其文件扩展名。</p>
<p>可以指定多 <strong>代</strong> 选项。</p>
<p>例如， <strong>-gen {um-default} </em> . tmh</strong> 表示对于 WPP 处理的每个 <strong>um-default</strong> 文件，它将生成 <strong>um-default. tmh</strong> 文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>扫描配置数据</p></td>
<td align="left"><p><strong>-scan：</strong><em>File</em></p></td>
<td align="left"><p>在不是配置文件的文件以及 defaultwpp.ini 中搜索配置数据（如自定义数据类型）。</p>
<p>将 <strong>begin_wpp 配置</strong> 和 <strong>end_wpp</strong> 字符串放置在配置数据的位置以进行标识。 使用与 defaultwpp.ini 中使用的配置数据相同的格式。</p>
<p>如果将配置数据添加到自定义配置文件，请使用 <strong>-ini</strong> 参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>备用配置文件</p></td>
<td align="left"><p><strong>-defwpp：</strong><em>path</em></p></td>
<td align="left"><p>指定另一个配置文件。 Wpp 使用此文件而不是 defaultwpp.ini 文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>其他配置文件</p></td>
<td align="left"><p><strong>-ini：</strong><em>路径</em></p></td>
<td align="left"><p>指定附加配置文件。 WPP 除了默认文件 defaultwpp.ini 之外，还使用指定的文件。</p>
<p>如果已创建新的配置文件来存储跟踪的配置数据，请使用此参数。 如果已将配置数据添加到另一类型的文件（如源文件或头文件），请使用 <strong>-scan</strong> 参数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwpp_build_processspanspan-idwpp_build_processspanwpp-build-process"></a><span id="wpp_build_process"></span><span id="WPP_BUILD_PROCESS"></span>WPP 生成过程


如果为驱动程序或用户模式应用程序启用 WPP，则生成驱动程序或应用程序将在编译驱动程序或应用程序文件之前调用 WPP 预处理器。

WPP 生成过程完成以下步骤：

1.  WPP 预处理器在每个源文件中处理 WPP 宏，并为每个源文件创建 [跟踪消息标头文件](trace-message-header-file.md) 。 源代码未直接修改。

2.  在 WPP 预处理器创建跟踪消息头文件后，C 预处理器以正常方式处理跟踪消息头文件中的内置 WPP 宏。

 

