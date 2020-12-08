---
title: 调试事件筛选器
description: 调试事件筛选器
keywords:
- 调试事件筛选器
- 异常，调试事件筛选器
- 事件，调试事件筛选器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55c77aad0a47f023a922fe96e26a9e96baa210c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823439"
---
# <a name="debug--event-filters"></a>调试 | 事件筛选器


## <span id="ddk_debug_event_filters_dbg"></span><span id="DDK_DEBUG_EVENT_FILTERS_DBG"></span>


单击 "**调试**" 菜单上的 "**事件筛选器**" 以打开 "**事件筛选器**" 对话框。 在此对话框中，可以配置 "中断状态" 和 "处理异常和事件的状态"。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

" **事件筛选器** " 对话框列出调试器可识别的所有事件。 您可以向随后将显示的列表添加已编号的例外。

若要更改事件的中断状态，请选择该事件，然后单击其中一个 **执行** 选项按钮 (**启用**、 **禁用**、 **输出** 或 **忽略**) 。

若要更改事件的处理状态，请选择该事件，然后单击 " **继续** " 选项按钮之一 (**处理** 或 **未处理**) 。

若要添加新的带编号的异常，请单击 " **添加**"。 当 " **异常筛选器** " 对话框出现时，输入异常代码，单击相应的 "中断状态和处理状态" 按钮，然后单击 **"确定"**。

若要删除已编号的异常，请选择该异常，然后单击 " **删除**"。 不能删除标准事件。

当你为 **Load 模块** 或 **卸载模块** 事件设置状态时，你可以将此状态限制为特定模块。 单击 " **参数**"，在 " **筛选器参数** " 对话框中输入模块名称或模块的基址，然后单击 **"确定"**。 指定基址时，可以使用 [通配符](string-wildcard-syntax.md) 。 如果未指定模块，则在加载或卸载任何模块时会发生中断。

设置 **调试对象输出** 事件的状态时，可以将此状态限制为特定的输出模式。 单击 " **参数**"，在 " **筛选器参数** " 对话框中输入输出模式，然后单击 **"确定"**。 如果未指定输出模式，则会对任何输出进行中断。

如果要设置在事件中断到调试器时执行的自动命令，请选择该事件，然后单击 " **命令**"。 将显示 " **筛选器命令** " 对话框。 在 " **命令** " 或 " **第二个命令** " 框中输入所需的任何命令。 使用分号分隔多个命令，并不要将这些命令用引号引起来。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关中断状态和处理状态、所有事件代码、所有事件的默认状态和控制此状态的其他方法的详细信息，请参阅 [控制异常和事件](controlling-exceptions-and-events.md)。

 

 





