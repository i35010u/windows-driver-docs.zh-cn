---
title: 调试事件筛选器
description: 调试事件筛选器
ms.assetid: ffa1241a-8a75-44ac-94b7-608393cf4138
keywords:
- 调试事件筛选器
- 异常，调试事件筛选器
- 事件，调试事件筛选器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc5a4284a241b2756acdef04bcbe55a133473bd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566367"
---
# <a name="debug--event-filters"></a>调试 | 事件筛选器


## <span id="ddk_debug_event_filters_dbg"></span><span id="DDK_DEBUG_EVENT_FILTERS_DBG"></span>


单击**事件筛选器**上**调试**菜单打开**事件筛选器**对话框。 在此对话框中，可以配置的中断状态和异常和事件的处理状态。

### <a name="span-iddialogboxspanspan-iddialogboxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>对话框

**事件筛选器**对话框框中列出的调试器识别的所有事件。 您可以向将显示的列表添加带编号的异常。

若要更改的事件的中断状态，请选择事件，然后单击之一**执行**选项按钮 (**已启用**，**禁用**，**输出**，或**忽略**)。

若要更改的事件的处理状态，请选择该事件，然后单击之一**继续**选项按钮 (**Handled**或**未处理**)。

若要添加新的带编号的异常，请单击**添加**。 当**异常筛选器**出现对话框，请输入异常代码，单击相应的按钮的中断状态和处理状态，然后单击**确定**。

若要删除带编号的异常，请选择该异常，然后单击**删除**。 无法删除标准事件。

如果设置的状态**负载模块**或**卸载模块**事件，可以限制此状态设置为特定模块。 单击**自变量**，输入模块的名称或中的模块的基址**筛选器参数**对话框中，然后单击**确定**。 可以使用[通配符](string-wildcard-syntax.md)时指定的基址。 如果未指定模块，在加载或卸载的任何模块时，会发生中断。

如果设置的状态**调试对象输出**事件，可以限制此状态设置为特定输出模式。 单击**自变量**，输入中的输出模式**筛选器参数**对话框中，然后单击**确定**。 如果未指定输出模式，在中断发生的任何输出。

如果你想要设置自动事件进入调试器时就会执行的命令，选择事件，然后单击**命令**。 **筛选器命令**对话框将出现。 输入想要登录到任何命令**命令**或**第二次命令**框。 使用分号分隔多个命令，不要将这些命令括在引号中。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关中断状态和处理状态、 所有事件代码、 所有事件和控制此状态的其他方法的默认状态的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)。

 

 





