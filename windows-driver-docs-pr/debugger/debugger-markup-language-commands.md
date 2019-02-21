---
title: 使用调试器标记语言
description: 调试程序命令可以提供以纯文本或在使用调试器标记语言 (DML) 的增强格式的输出。 已增强，DML 的输出中包括的链接。
ms.assetid: 70DDC56F-614F-43B7-B325-91984B74AECF
keywords:
- 调试器标记语言
- DML
- 增强的调试器命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a076a9d17b8eb5626096386b8c96e138091f69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533986"
---
# <a name="using-debugger-markup-language"></a>使用调试器标记语言


调试程序命令可以提供以纯文本或在使用调试器标记语言 (DML) 的增强格式的输出。 已增强，DML 的输出包括链接，可单击以执行相关的命令。

DML 是可用在 Windows 10 及更高版本。

**DML 支持命令**

能够生成 DML 输出中使用以下命令：

-   [**.dml\_start**](-dml-start.md)
-   [**.dml\_flow**](-dml-flow.md)
-   [**!dml\_proc**](-dml-proc.md)
-   [**lmD**](lm--list-loaded-modules-.md)
-   [**kM**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)
-   [**.chain /D**](-chain--list-debugger-extensions-.md)
-   [**.help 获取 /D**](-help--meta-command-help-.md)
-   [**.printf /D**](-printf.md)

[ **LmD** ](lm--list-loaded-modules-.md)命令是一个示例是能够提供 DML 输出的命令。 **LmD**命令显示已加载的模块的列表。 如图所示，每个模块名称将是您可以单击以获取有关模块的更多详细的信息的链接。

![lmd 输出的屏幕截图](images/dmlcommands01.png)

下图显示单击的结果**usbuhci**链接。 输出包括使您能够进一步浏览 usbuhci 模块的详细信息的其他链接。

![模块详细信息的屏幕截图](images/dmlcommands02.png)

**打开和关闭 DML**

[ **.Prefer\_dml** ](-prefer-dml.md)命令会启用 DML，打开或关闭。 当启用 DML 时 (.prefer\_dml 1)，能够生成 DML 命令输出会默认情况下生成 DML 输出。

### <a name="span-idconsoleenhancementsspanspan-idconsoleenhancementsspanspan-idconsoleenhancementsspanconsole-enhancements"></a><span id="Console_Enhancements"></span><span id="console_enhancements"></span><span id="CONSOLE_ENHANCEMENTS"></span>控制台增强功能

所有 Windows 调试器现支持 DML 分析命令输出区域。 在 windbg 中命令窗口支持所有 DML 行为，并将显示颜色、 字体样式和链接。 使用颜色模式已启用，则返回 true 的控制台中运行时，控制台调试器，ntsd、 cdb 和 kd，仅支持 DML，和唯一的颜色属性。 通过重定向 I/O 的调试器，ntsd – d 或 remote.exe 会话不会显示任何颜色。

### <a name="span-idconsoledebuggercolormodespanspan-idconsoledebuggercolormodespanspan-idconsoledebuggercolormodespanconsole-debugger-color-mode"></a><span id="Console_Debugger_Color_Mode"></span><span id="console_debugger_color_mode"></span><span id="CONSOLE_DEBUGGER_COLOR_MODE"></span>控制台调试器颜色模式

控制台调试器、 ntsd、 cdb 和 kd 现显示彩色的输出时，则返回 true 的控制台中运行的能力。 这不是默认值，它需要显式启用通过 tools.ini 颜色模式。 新 col\_模式下&lt;true | false&gt;中 tools.ini 令牌控制颜色模式设置。 有关使用 tools.ini 文件的详细信息，请参阅[配置 tools.ini](configuring-tools-ini.md)

启用颜色模式调试器可以生成彩色的输出。 默认情况下大多数颜色未设置，而是默认为当前控制台颜色。

### <a name="span-idwindbgcommandbrowserwindowspanspan-idwindbgcommandbrowserwindowspanspan-idwindbgcommandbrowserwindowspan-windbg-command-browser-window"></a><span id="_Windbg_Command_Browser_Window"></span><span id="_windbg_command_browser_window"></span><span id="_WINDBG_COMMAND_BROWSER_WINDOW"></span> Windbg 命令浏览器窗口

在 Windows 10 和更高版本的 Windbg 命令浏览器窗口分析并显示 DML。 所有标记，如&lt;链接&gt;， &lt;exec&gt;外观修改系统完全支持。

若要开始使用 WinDbg 中的菜单命令浏览器会话，请选择**视图**，**命令浏览器**。 .Browse&lt;命令&gt;在命令窗口将打开一个新的命令浏览器窗口并执行给定的命令。 有关详细信息请参阅[使用命令浏览器窗口在 WinDbg 中](command-browser-window.md)。 此外可以使用 Ctrl + N 打开一个新的命令浏览器窗口。

命令浏览器窗口谨慎地模拟 web 浏览器中，使用下拉列表历史记录和上一个/下一个按钮的行为。 历史记录下拉列表仅显示最后二十个命令，但完整历史记录仍保留，以便您可以通过在命令获取下拉列表以显示较旧的历史记录。

您可以根据需要同时打开的任意多个命令窗口。 命令窗口保留在工作区中，但仅将保存当前的命令;不放置在历史记录。

WinDbg**视图**菜单还拥有**设置浏览器启动命令**选项，这样用户就可以开始时，设置新的浏览器窗口的首选的命令，例如.dml\_开始。 此命令保存在工作区中。

一个**新的命令**子窗口位于**视图**菜单来保存感兴趣的命令。 选择新的命令将新的浏览器打开与给定命令。 将窗口的当前命令添加到新的命令的列表的浏览器窗口的上下文菜单上没有菜单项。 在工作区中保留的最新命令的列表。

命令浏览器窗口以同步方式执行该命令，因此不会显示输出直到完成该命令。 长时间运行的命令不会显示任何内容之前已完成。

链接具有类似于右键单击上下文菜单右键单击上下文菜单在 web 浏览器中。 可以在新的浏览器窗口中打开链接。 链接的命令可以复制到剪贴板，以便使用。

单击要设置为自动刷新或手动刷新命令浏览器窗口的标题栏右上角附近的图标。 自动刷新浏览器将自动重新运行其命令在调试器状态更改。 这会使输出实时但代价是会执行该命令上的所有更改。 自动刷新在默认情况下处于打开状态。 如果不需要处于活动状态，在浏览器窗口的上下文菜单可用于禁用自动刷新。

由于命令执行引擎，不通过用户界面，用户界面特定的命令，如[ **.cls （清除屏幕）**](-cls--clear-screen-.md)，命令浏览器中使用时，将返回中的语法错误windows。 它还意味着，当用户界面是远程客户端、 服务器不是由客户端，将执行命令和命令输出会显示服务器状态。

命令的浏览器窗口可以运行任何调试器命令，它不一定要生成 DML 命令。 可以使用浏览器窗口具有一组任意的供使用的有效命令。

## <a name="span-idcustomizingdmlspanspan-idcustomizingdmlspanspan-idcustomizingdmlspancustomizing-dml"></a><span id="Customizing_DML"></span><span id="customizing_dml"></span><span id="CUSTOMIZING_DML"></span>自定义的 DML


DML 定义少量的标记，可以包含在命令输出。 是一个例子&lt;链接&gt;标记。 您可以体验&lt;链接&gt;标记 （和其他 DML 标记），通过使用[ **.dml\_启动**](-dml-start.md)并[ **.browse**](-browse--display-command-in-browser-.md)命令。 该命令 **.browse.dml\_启动** *filepath*执行 DML 文件中存储的命令。 中显示的输出[命令浏览器窗口](command-browser-window.md)而不是常规的命令窗口。

假设文件 c:\\DmlExperiment.txt 包含以下行。

```text
My DML Experiment
<link cmd="lmD musb*">List modules that begin with usb.</link>
```

以下命令命令浏览器窗口中显示的文本和链接。

```dbgcmd
.browse .dml_start c:\Dml_Experiment.txt
```

![dml 文件输出的屏幕截图](images/dmlcommands03.png)

如果单击**列表的开头 usb 模块**链接，请参阅下图类似的输出。

![模块列表的屏幕截图](images/dmlcommands04.png)

DML 自定义的全面讨论和 DML 标记的完整列表，请参阅[自定义调试器输出使用 DML](customizing-debugger-output-using-dml.md)。

 

 





