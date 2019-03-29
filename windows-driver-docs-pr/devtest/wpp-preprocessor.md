---
title: WPP 预处理器
description: WPP 预处理器
ms.assetid: 92bcb2c4-f6de-4704-8f5c-9a2e5901616a
keywords:
- Windows 软件跟踪预处理器 WDK，选项
- WPP 软件跟踪 WDK，选项
- WPP 预处理器 WDK
- Windows 软件跟踪预处理器 WDK，调用预处理器
- WPP 软件跟踪 WDK、 调用预处理器
- Windows 软件跟踪预处理器 WDK、 生成过程
- WPP 软件跟踪 WDK，生成过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85b399b4e2490cbec2ec4fd6a3c3d02f9d832d91
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464347"
---
# <a name="wpp-preprocessor"></a>WPP 预处理器


本部分介绍*Windows 软件跟踪预处理器*，通常称为 WPP 预处理器。

## <a name="span-idinvokingthewpppreprocessorspanspan-idinvokingthewpppreprocessorspan-invoking-the-wpp-preprocessor"></a><span id="invoking_the_wpp_preprocessor"></span><span id="INVOKING_THE_WPP_PREPROCESSOR"></span> 调用 WPP 预处理器


可以调用预处理器使用 Visual Studio 和 MSBuild 环境 WPP。

**若要调用 WPP 预处理器**

1.  右键单击解决方案资源管理器中的驱动程序项目，然后单击**属性。**
2.  在项目属性页中，单击**配置属性**单击**WPP 跟踪**
3.  下**常规**，请设置**运行 WPP**选项设置为**是**。
4.  下**命令行**，可以添加下面的选项自定义跟踪行为。

    例如，在**WPP 跟踪**，可以指定单个**扫描配置数据**文件。

    如果你需要提供多个一个配置文件，例如若要指定自定义数据类型，引用你的文件中**命令行**使用 **-扫描**选项，例如：

    ```
    -scan:"$(KMDF_INC_PATH)\$(KMDF_VER_PATH)\WdfTraceEnums.h"
    ```

有关生成过程的详细信息，请参阅[TraceWPP 任务](tracewpp-task.md)并[WDK 和 Visual Studio 构建环境](wdk-and-visual-studio-build-environment.md)。

此外可以通过使用 TraceWPP 工具 (TraceWPP.exe)，从生成环境中运行单独的预处理器。 此工具位于 WDK 的 bin/x86 子目录中。

## <a name="span-idwpptracinggeneraloptionsspanspan-idwpptracinggeneraloptionsspanspan-idwpptracinggeneraloptionsspanwpp-tracing-general-options"></a><span id="WPP_Tracing_General_Options"></span><span id="wpp_tracing_general_options"></span><span id="WPP_TRACING_GENERAL_OPTIONS"></span>WPP 跟踪的常规选项


下表描述了预处理器 WPP 的选项。 在 Visual Studio 中为你的项目，或用作 TraceWPP 工具的参数使用 WPP 跟踪属性页中，可以配置这些选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WPP 跟踪选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 WPP</p></td>
<td align="left"><p>如果为 true，将调用 WPP。</p></td>
</tr>
<tr class="even">
<td align="left"><p>启用最小重新生成</p></td>
<td align="left"><p>如果为 true，则执行跟踪的增量生成;如果为 false，则执行重新生成。</p></td>
</tr>
</tbody>
</table>

 

## <span id="run_wpp_options"></span><span id="RUN_WPP_OPTIONS"></span>


## <a name="span-idfunctionandmacrooptionsspanspan-idfunctionandmacrooptionsspanspan-idfunctionandmacrooptionsspanfunction-and-macro-options"></a><span id="Function_and_Macro_Options"></span><span id="function_and_macro_options"></span><span id="FUNCTION_AND_MACRO_OPTIONS"></span>函数和宏选项


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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>预处理器定义</p></td>
<td align="left"><p><strong>-D</strong><em>Macro</em></p></td>
<td align="left"><p>将添加<strong>#定义</strong><em>宏</em>到生成文件的开头位置<em>宏</em>是宏的名称。</p>
<p>此选项具有相同的效果<strong>/D</strong> （定义了一个宏） 编译器选项。 包含它是为了确保，它定义在 TMH 文件的开头为有效。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p><strong>-D</strong><em>宏</em><strong>=</strong><em>扩展</em></p></td>
<td align="left"><p>将添加<strong>#定义</strong><em>宏扩展</em>到生成文件的开头位置<em>宏</em>是宏的名称和<em>扩展</em>是扩展的值。</p>
<p>此选项具有相同的效果<strong>/D</strong> （定义了一个宏） 编译器选项。 包含它是为了确保，它定义在 TMH 文件的开头为有效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>跟踪内核模式组件</p></td>
<td align="left"><p><strong>-km</strong></p></td>
<td align="left"><p>定义跟踪内核模式组件的 WPP_KERNEL_MODE 宏。 默认情况下，要跟踪仅用户模式组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>启用 Dll 宏</p></td>
<td align="left"><p><strong>-dll</strong></p></td>
<td align="left"><p>定义 WPP_DLL 宏，这将导致每次调用 WPP_INIT_TRACING 时要初始化的 WPP 数据结构。 否则，只有一次初始化结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>指定控件 GUID</p></td>
<td align="left"><p><strong>-ctl:</strong><em>GUID</em></p></td>
<td align="left">定义<a href="https://msdn.microsoft.com/library/windows/hardware/ff556186" data-raw-source="[WPP_CONTROL_GUIDS](https://msdn.microsoft.com/library/windows/hardware/ff556186)">WPP_CONTROL_GUIDS</a>具有指定的宏<a href="control-guid.md" data-raw-source="[control GUID](control-guid.md)">控制 GUID</a>和 WPP_DEFINE_BIT 项名为错误、 发生异常和噪音。
<p>这是将宏添加到源代码文件的替代方法。</p>
<p><em>GUID</em>表示控件的 GUID。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsearchandformattingoptionsspanspan-idsearchandformattingoptionsspanspan-idsearchandformattingoptionsspansearch-and-formatting-options"></a><span id="Search_and_Formatting_Options"></span><span id="search_and_formatting_options"></span><span id="SEARCH_AND_FORMATTING_OPTIONS"></span>搜索和格式设置选项


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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>忽略感叹号</p></td>
<td align="left"><p><strong>-noshrieks</strong></p></td>
<td align="left"><p>指示 WPP 忽略感叹号，也称为"shrieks。"</p>
<p>使用在复杂的格式，如 %！ 时间戳 ！ %。 默认情况下，感叹号所需，WPP 尝试将其解释。</p></td>
</tr>
<tr class="even">
<td align="left"><p>数值基本的编号的格式字符串</p></td>
<td align="left"><p><strong>-argbase:</strong><em>数量</em></p></td>
<td align="left"><p>将生成数值基准的编号的格式字符串，如"%1 ！ d ！，%2 2!s ！。" 默认值为 1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>函数以生成跟踪消息</p></td>
<td align="left"><p><strong>-f u n c:</strong><em>FunctionDescription</em></p></td>
<td align="left"><p>指定的替代方法<a href="https://msdn.microsoft.com/library/windows/hardware/ff544918" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544918)"> <strong>DoTraceMessage</strong> </a>宏。 然后可以使用这些函数以生成跟踪消息。</p>
<p>例如，可以定义一个函数，如指定标志和跟踪消息的级别：</p>
<pre space="preserve"><code>-func (DoMyTraceMessage(LEVEL,FLAGS,MSG,...)</code></pre>
<p>可以使用的多个实例<strong>-func</strong>选项。</p>
<p>此选项是在本地配置文件中指定函数说明的替代方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p>指定搜索字符串</p></td>
<td align="left"><p><strong>-lookfor:</strong><em>字符串</em></p></td>
<td align="left"><p>指示 WPP 搜索要启动跟踪的指定字符串的源代码文件。 默认情况下，WPP 搜索字符串"WPP_INIT_TRACING。"</p>
<p>这是一个高级的选项的用户正在编写他们自己的模板。</p>
<p>例如，在 default.tpl:</p>
<pre space="preserve"><code><code>IF FOUND WPP_INIT_TRACING</code>
 <code>INCLUDE um-init.tpl</code>
<code>ENDIF</code></code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p>指定模块名称</p></td>
<td align="left"><p><strong>-p:</strong><em>字符串</em></p></td>
<td align="left"><p>指定的备选友好名称的<a href="message-guid.md" data-raw-source="[message GUID](message-guid.md)">消息 GUID</a>的消息从此<a href="trace-provider.md" data-raw-source="[trace provider](trace-provider.md)">跟踪提供程序</a>。 默认情况下，消息 GUID 的友好名称是目录的在其中生成跟踪提供程序的名称。</p>
<p>消息的 GUID 的友好名称，默认情况下显示，在<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">跟踪消息前缀</a>变量，由表示<strong>%1</strong>。 可以使用此参数以将字符串添加到前缀，以帮助用户标识跟踪提供程序，如跟踪提供程序，包括跟踪提供程序，该模块的名称或通过创建严重性级别实现的项目的名称的友好名称几跟踪提供程序。 此信息可帮助用户将位于不同的文件或不同的路径中的相关的跟踪提供程序相关联。</p>
<p><strong>-P</strong>参数需要 WPP 包含适用于 Windows Vista 中 Windows Driver Kit (WDK) 的版本和更高版本的 WDK。 <strong>-P</strong>参数适用于 Windows 2000 和更高版本的 Windows。</p>
<p>示例：</p>
<pre space="preserve"><code>-p:TraceDrv
-p:AudioModule</code></pre></td>
</tr>
</tbody>
</table>

 

## <a name="span-idfileoptionsspanspan-idfileoptionsspanspan-idfileoptionsspanfile-options"></a><span id="File_Options"></span><span id="file_options"></span><span id="FILE_OPTIONS"></span>文件选项


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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>附加包含目录</p></td>
<td align="left"><p><strong>-I</strong> <em>Path1</em><strong>[;</strong><em>Path2</em><strong>]</strong></p></td>
<td align="left"><p>指定要添加到包含路径; 的一个或多个目录用如果多个分号隔开。 与-相同<strong>cfgdir</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>配置目录</p></td>
<td align="left"><p><strong>-cfgdir:</strong><em>Path1</em><strong>[;</strong><em>Path2</em><strong>]</strong></p></td>
<td align="left"><p>指定的配置和模板文件的位置。</p>
<p><em>Path1</em>并<em>Path2</em>表示到目录的完全限定的路径。 可以指定多个路径。 默认值为本地目录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>文件扩展名</p></td>
<td align="left"><p><strong>-ext:.</strong> <em>ext1</em> <strong>[.</strong><em>ext2</em><strong>]</strong></p></td>
<td align="left"><p>为源文件指定 WPP 可识别的文件类型。 WPP 将忽略具有不同的文件扩展名的文件。</p>
<p>默认情况下，WPP 识别仅.c、.c + +、.cpp 和.cxx 文件。</p>
<p>此选项允许您为 WPP 使用默认设置，而无需删除或重命名 WPP 不使用，如.rc 资源文件和.mc 文件。</p>
<p>例如，若要将跟踪添加到 c + + 文件和标头 (.h) 文件，使用以下命令：</p>
<p><strong>-ext:.cpp.CPP.h.H</strong></p>
<p>此外，若要为 c + + 和标头文件不同名称的 TMH 文件，使用<strong>-preserveext</strong>选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>保留文件扩展</p></td>
<td align="left"><p><strong>-preserveext:</strong> <em>.ext1</em><strong>[.</strong><em>ext2</em><strong>]</strong></p></td>
<td align="left"><p>创建 TMH 文件时保留指定的文件扩展名。</p>
<p>默认情况下，命名为 TMH 文件的所有文件类型<em>文件名</em>.tmh。 导致此问题文件名称冲突具有多个具有相同名称的源代码文件。</p>
<p>例如，默认情况下，C 文件 (.c) TMH 文件和标头 (.h) 文件将被命名为&lt;文件名&gt;.tmh。 通过使用<strong>-preserveext:.c.h</strong>，TMH 文件被命名为&lt;filename&gt;。 c.tmh 并&lt;文件名&gt;。 h.tmh。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>输出目录</p></td>
<td align="left"><strong>-odir:</strong> <em>路径</em></td>
<td align="left"><p>指定 WPP 创建的输出文件的目录。</p>
<p><em>路径</em>是目录的完全限定的路径。 默认值为本地目录。</p></td>
</tr>
<tr class="even">
<td align="left"><p>指定模板文件</p></td>
<td align="left"><p><strong>-常规 {File.tpl}<em>。 ext</strong></p></td>
<td align="left"><p>有关 WPP 处理大括号之间指定的名称与每个源文件{}，创建另一个文件扩展名的指定的文件的名称。</p>
<p>File.tpl 表示源代码文件。 *.ext 表示创建的文件和其文件扩展名的类型。</p>
<p>可以指定多个<strong>-常规</strong>选项。</p>
<p>例如， <strong>-常规 {um default.tpl}</em>.tmh</strong>意味着对于每个<strong>um default.tpl</strong>文件 WPP 处理时，它会生成<strong>um default.tmh</strong>文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>扫描配置数据</p></td>
<td align="left"><p><strong>-扫描：</strong><em>文件</em></p></td>
<td align="left"><p>配置数据，例如自定义数据类型，以及 defaultwpp.ini 不是配置文件的文件中搜索。</p>
<p>位置<strong>begin_wpp config</strong>并<strong>end_wpp</strong>配置数据，以将其标识的字符串。 配置数据使用相同的格式，如 defaultwpp.ini 中使用。</p>
<p>如果配置数据添加到自定义配置文件时，使用<strong>-ini</strong>参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>备用配置文件</p></td>
<td align="left"><p><strong>-defwpp:</strong><em>path</em></p></td>
<td align="left"><p>指定的备用配置文件。 Wpp 而不是 defaultwpp.ini 文件使用此文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>其他配置文件</p></td>
<td align="left"><p><strong>-ini:</strong><em>路径</em></p></td>
<td align="left"><p>指定的其他配置文件。 WPP 除了默认文件中，使用指定的文件 defaultwpp.ini。</p>
<p>已创建新的配置文件来存储跟踪的配置数据时，请使用此参数。 如果配置数据添加到另一个类型的文件，如源文件或头文件，使用<strong>-扫描</strong>参数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwppbuildprocessspanspan-idwppbuildprocessspanwpp-build-process"></a><span id="wpp_build_process"></span><span id="WPP_BUILD_PROCESS"></span>WPP 生成过程


之前驱动程序或应用程序文件进行编译，如果驱动程序或用户模式应用程序启用了 WPP，构建的驱动程序或应用程序调用预处理器 WPP。

WPP 生成过程完成以下步骤：

1.  WPP 预处理器处理每个源文件中的 WPP 宏，并创建[跟踪消息标头文件](trace-message-header-file.md)为每个源文件。 不直接修改源代码。

2.  预处理器 WPP 创建跟踪消息标头文件后，C 预处理器以正常方式处理跟踪消息标头文件中的内置 WPP 宏。

 

 





