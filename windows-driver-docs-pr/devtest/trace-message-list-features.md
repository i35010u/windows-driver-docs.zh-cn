---
title: 跟踪消息列表功能
description: 跟踪消息列表功能
keywords:
- 跟踪消息列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b299ca1ff4fb26436b672644921a50b8078db9c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840401"
---
# <a name="trace-message-list-features"></a>跟踪消息列表功能


本主题介绍跟踪消息列表的功能。 您可以使用这些功能来自定义列表。

### <a name="span-iddisplaying_and_hiding_columnsspanspan-iddisplaying_and_hiding_columnsspandisplaying-and-hiding-columns"></a><span id="displaying_and_hiding_columns"></span><span id="DISPLAYING_AND_HIDING_COLUMNS"></span>显示和隐藏列

若要显示和隐藏跟踪消息列表的列，请右键单击列标题行中的任意位置。 在出现的快捷菜单中，会显示选中的属性;未选中的属性被隐藏。 若要显示或隐藏属性，请从快捷菜单中选择它。

您可以使用此过程来显示有关跟踪消息的有价值的信息，包括函数名称和生成消息的源代码中的行号。

### <a name="span-idsaving_the_column_configurationspanspan-idsaving_the_column_configurationspansaving-the-column-configuration"></a><span id="saving_the_column_configuration"></span><span id="SAVING_THE_COLUMN_CONFIGURATION"></span>保存列配置

默认情况下，TraceView 显示所选列。 如果希望显示和隐藏不同的列，可以将列配置保存为新的默认配置。

若要保存新的列配置，请执行以下操作：

1.  在跟踪消息列表中，右键单击任意列标题。

2.  单击 " **另存为默认值**"。

### <a name="span-idsorting_by_columnspanspan-idsorting_by_columnspansorting-by-column"></a><span id="sorting_by_column"></span><span id="SORTING_BY_COLUMN"></span>按列排序

若要按列中的值进行排序，请单击列标题。 重复单击列标题时，该列将在该列中值的升序和降序之间切换。 默认情况下，跟踪消息列表按 "**消息 \#** " 列中的值进行排序。

### <a name="span-idautofit_columnsspanspan-idautofit_columnsspanautofit-columns"></a><span id="autofit_columns"></span><span id="AUTOFIT_COLUMNS"></span>自动调整列

若要将每列的宽度调整到该列中数据的宽度，请在跟踪消息列表中右键单击任何跟踪消息行 (除了列标题) ，然后单击 " **自动调整列**"。

### <a name="span-idclear_displayspanspan-idclear_displayspanclear-display"></a><span id="clear_display"></span><span id="CLEAR_DISPLAY"></span>清除显示

若要从显示中删除所有跟踪消息，请在跟踪消息列表中右键单击任何跟踪消息行 (除了列标题) ，然后单击 " **清除显示**"。

清除显示不会从跟踪日志或输出文件中删除跟踪消息。 但是，如果消息是由实时跟踪会话生成，而不是保存在日志或输出文件中，则您将无法恢复它们。

### <a name="span-idcopying_trace_messagesspanspan-idcopying_trace_messagesspancopying-trace-messages"></a><span id="copying_trace_messages"></span><span id="COPYING_TRACE_MESSAGES"></span>复制跟踪消息

若要从跟踪消息列表复制跟踪消息，请执行以下操作：

1.  选择要复制的跟踪消息。 你可以使用 SHIFT + 单击来选择连续消息，或按 CTRL + 单击来复制不连续的消息。

2.  按 CTRL + C。 或者，右键单击任意选定跟踪消息的任何单元，然后单击 " **复制**"。

消息是以制表符分隔的格式复制的。 可以将其粘贴到文本文件或电子表格文件中，供以后使用。

有关保存跟踪消息的详细信息，请参阅 [创建跟踪日志的文本版本](creating-text-versions-of-trace-logs.md)。

 

 





