---
title: 使用调试器标记语言
description: 调试器命令可以提供纯文本格式的输出，也可以提供使用调试器标记语言 (DML) 的增强格式的输出。 通过 DML 增强的输出包含链接。
keywords:
- 调试器标记语言
- DML
- 增强的调试器命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c112ab824898c9b503e8b8b10b252e4fe93cee7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809707"
---
# <a name="using-debugger-markup-language"></a>使用调试器标记语言


调试器命令可以提供纯文本格式的输出，也可以提供使用调试器标记语言 (DML) 的增强格式的输出。 通过 DML 增强的输出包含可用于执行相关命令的链接。

DML 适用于 Windows 10 及更高版本。

**支持 DML 的命令**

以下命令可以生成 DML 输出：

-   [**dml \_ start**](-dml-start.md)
-   [**dml \_ flow**](-dml-flow.md)
-   [**！ dml \_ proc**](-dml-proc.md)
-   [**lmD**](lm--list-loaded-modules-.md)
-   [**千米**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)
-   [**。链式/D**](-chain--list-debugger-extensions-.md)
-   [**。 help/D**](-help--meta-command-help-.md)
-   [**printf/D**](-printf.md)

[**LmD**](lm--list-loaded-modules-.md)命令是可以提供 DML 输出的命令示例。 **LmD** 命令显示加载的模块的列表。 如下图所示，每个模块名称都是一个链接，你可以单击该链接来获取有关模块的更多详细信息。

![lmd 输出的屏幕截图](images/dmlcommands01.png)

下图显示了单击 **usbuhci** 链接的结果。 输出包含其他链接，使你能够浏览 usbuhci 模块的更多详细信息。

![模块详细信息的屏幕截图](images/dmlcommands02.png)

**打开和关闭 DML**

[**。首选 \_ dml**](-prefer-dml.md)命令打开或关闭 dml。 当启用 DML ( 时。更倾向于 \_ dml 1) ，能够生成 dml 输出的命令将默认生成 dml 输出。

### <a name="span-idconsole_enhancementsspanspan-idconsole_enhancementsspanspan-idconsole_enhancementsspanconsole-enhancements"></a><span id="Console_Enhancements"></span><span id="console_enhancements"></span><span id="CONSOLE_ENHANCEMENTS"></span>控制台增强功能

现在，所有 Windows 调试器都具有支持 DML 分析的命令输出区域。 在 windbg 中，命令窗口支持所有 DML 行为，并将显示颜色、字体样式和链接。 控制台调试，ntsd，cdb 和 kd 仅支持 DML 的颜色属性，并且仅在启用了颜色模式的真正控制台中运行时才支持。 具有重定向 i/o、ntsd – d 或 remote.exe 会话的调试器不会显示任何颜色。

### <a name="span-idconsole_debugger_color_modespanspan-idconsole_debugger_color_modespanspan-idconsole_debugger_color_modespanconsole-debugger-color-mode"></a><span id="Console_Debugger_Color_Mode"></span><span id="console_debugger_color_mode"></span><span id="CONSOLE_DEBUGGER_COLOR_MODE"></span>控制台调试器颜色模式

控制台调试，ntsd，cdb 和 kd 现在能够在真正的控制台中运行时显示彩色输出。 这不是默认值，它要求通过 tools.ini 显式启用颜色模式。 New col \_ mode &lt; true | false &gt; 标记 tools.ini 控制颜色模式设置。 有关使用 tools.ini 文件的详细信息，请参阅 [配置 tools.ini](configuring-tools-ini.md)

启用颜色模式后，调试器可以生成彩色输出。 默认情况下，大多数颜色未设置，而是默认设置为当前控制台颜色。

### <a name="span-id_windbg_command_browser_windowspanspan-id_windbg_command_browser_windowspanspan-id_windbg_command_browser_windowspan-windbg-command-browser-window"></a><span id="_Windbg_Command_Browser_Window"></span><span id="_windbg_command_browser_window"></span><span id="_WINDBG_COMMAND_BROWSER_WINDOW"></span> Windbg 命令浏览器窗口

在 Windows 10 和更高版本中，该命令浏览器窗口分析并显示 DML。 完全支持所有标记 &lt; ，如 link &gt; 、 &lt; exec &gt; 和外观修改。

若要使用 WinDbg 中的菜单启动命令浏览器会话，请选择 " **视图**"、" **命令浏览器**"。 &lt; &gt; 命令窗口中的 .browser 命令将打开一个新的命令浏览器窗口并执行给定的命令。 有关详细信息，请参阅 [在 WinDbg 中使用命令浏览器窗口](command-browser-window.md)。 还可以使用 Ctrl + N 打开新的命令浏览器窗口。

"命令浏览器" 窗口特意模拟 web 浏览器的行为，其中包含下拉历史记录和 "上一个/下一个" 按钮。 "历史记录" 下拉箭头仅显示最后二十个命令，但完整的历史记录将保留，因此，返回到下拉菜单后即可显示较旧的历史记录。

您可以根据自己的需要打开任意数量的命令窗口。 命令窗口保留在工作区中，但仅保存当前命令;不保留历史记录。

"WinDbg **视图** " 菜单具有 " **设置浏览器启动" 命令** 选项，该选项允许用户为新的浏览器窗口设置一个首选项以开始使用，如 dml \_ Start。 此命令保存在工作区中。

"**查看**" 菜单上提供了 "**最新命令**" 子窗口，用于保存相关命令。 选择 "最近使用的命令" 将打开具有给定命令的新浏览器。 浏览器窗口的上下文菜单中有一个菜单项，可将该窗口的当前命令添加到最近使用的命令列表中。 最近使用的命令列表保存在工作区中。

命令浏览器窗口以同步方式执行命令，因此在命令完成之前，不会显示输出。 长时间运行的命令在完成之前将不会显示任何内容。

链接具有类似于在 web 浏览器中右键单击上下文菜单的右键单击上下文菜单。 可以在新的浏览器窗口中打开链接。 可以将链接的命令复制到剪贴板以供使用。

单击标题栏右上角附近的图标可将命令浏览器窗口设置为自动刷新或手动刷新。 自动刷新浏览器会在调试器状态更改时自动重新运行其命令。 这会使输出保持活动状态，但会在执行所有更改时执行命令。 默认情况下启用自动刷新。 如果浏览器无需成为现场，则可以使用窗口的上下文菜单来禁用自动刷新。

由于命令由引擎执行，而不是由用户界面执行，因此，特定于用户界面的命令（如 [**(明文屏幕)**](-cls--clear-screen-.md)）将在命令浏览器窗口中使用时返回中的语法错误。 这也意味着，当用户界面为远程客户端时，该命令将由服务器执行，而不是由客户端执行，命令输出将显示服务器状态。

命令浏览器窗口可以运行任何调试器命令，它不一定是生成 DML 的命令。 您可以使用浏览器窗口为任意一组活动的命令使用。

## <a name="span-idcustomizing_dmlspanspan-idcustomizing_dmlspanspan-idcustomizing_dmlspancustomizing-dml"></a><span id="Customizing_DML"></span><span id="customizing_dml"></span><span id="CUSTOMIZING_DML"></span>自定义 DML


DML 定义可包含在命令输出中的一小部分标记。 例如， &lt; 链接 &gt; 标记。 您可以 &lt; &gt; 使用 [**DML \_ start**](-dml-start.md) 和 [**. browse**](-browse--display-command-in-browser-.md) 命令来试验 link 标记 (和其他 dml 标记) 。 Command. node.js **\_ start** *FILEPATH* 执行存储在 dml 文件中的命令。 输出显示在 [命令浏览器窗口](command-browser-window.md) 中，而不是常规的命令窗口中。

假设文件 c： \\DmlExperiment.txt 包含以下行。

```text
My DML Experiment
<link cmd="lmD musb*">List modules that begin with usb.</link>
```

以下命令在命令浏览器窗口中显示文本和链接。

```dbgcmd
.browse .dml_start c:\Dml_Experiment.txt
```

![dml 文件输出的屏幕截图](images/dmlcommands03.png)

如果单击 " **列出以 usb 链接开头的模块** "，将看到类似于下图的输出。

![模块列表的屏幕截图](images/dmlcommands04.png)

有关 DML 自定义和 DML 标记的完整列表的详细讨论，请参阅 [使用 DML 自定义调试器输出](customizing-debugger-output-using-dml.md)。

 

 





