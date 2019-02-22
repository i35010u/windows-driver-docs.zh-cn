---
title: 跟踪消息列表的功能
description: 跟踪消息列表的功能
ms.assetid: c640626d-6d64-45c4-861f-6e2f20b7dfb1
keywords:
- 跟踪消息列表 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5912df03c0a6c848fe9dd5f5d73698b796fca06a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541701"
---
# <a name="trace-message-list-features"></a>跟踪消息列表的功能


本主题介绍跟踪消息列表的功能。 这些功能可用于自定义的列表。

### <a name="span-iddisplayingandhidingcolumnsspanspan-iddisplayingandhidingcolumnsspandisplaying-and-hiding-columns"></a><span id="displaying_and_hiding_columns"></span><span id="DISPLAYING_AND_HIDING_COLUMNS"></span>显示和隐藏列

若要显示和隐藏列的跟踪消息列表，请右键单击列标题行中的任意位置。 快捷方式菜单中，检查将显示属性;取消选中的属性被隐藏。 若要显示或隐藏属性，请从快捷菜单中选择它。

此过程可用于显示有关跟踪消息，包括生成消息的源代码中的函数名称和行号的重要信息。

### <a name="span-idsavingthecolumnconfigurationspanspan-idsavingthecolumnconfigurationspansaving-the-column-configuration"></a><span id="saving_the_column_configuration"></span><span id="SAVING_THE_COLUMN_CONFIGURATION"></span>正在保存列配置

默认情况下，TraceView 显示所选的列。 如果想要具有不同的列显示和隐藏的可以用以下方法将列配置保存为新的默认配置。

若要保存新的列配置，请执行以下操作：

1.  在跟踪消息列表中，右键单击任意列标题。

2.  单击**另存为默认**。

### <a name="span-idsortingbycolumnspanspan-idsortingbycolumnspansorting-by-column"></a><span id="sorting_by_column"></span><span id="SORTING_BY_COLUMN"></span>按列排序

若要按列中的值排序，请单击列标题。 当您单击列标题可在升降时，列在升序和降序，该列中的值之间进行切换。 默认情况下，跟踪消息列表进行排序中的值**Msg\#** 列。

### <a name="span-idautofitcolumnsspanspan-idautofitcolumnsspanautofit-columns"></a><span id="autofit_columns"></span><span id="AUTOFIT_COLUMNS"></span>自动调整列

若要调整为宽度，该列中数据的每个列的宽度，请右键单击任何跟踪消息 （而不是列标题） 列表中的行跟踪消息，然后单击**自动调整列**。

### <a name="span-idcleardisplayspanspan-idcleardisplayspanclear-display"></a><span id="clear_display"></span><span id="CLEAR_DISPLAY"></span>清晰地显示

若要从显示中删除所有跟踪消息，请右键单击任何跟踪消息 （而不是列标题） 列表中的行跟踪消息，然后单击**清晰显示**。

清除显示不会删除跟踪日志或输出文件中跟踪消息。 但是，如果消息正在生成由实时跟踪会话，并且不保存在日志或输出文件中，您将无法恢复它们。

### <a name="span-idcopyingtracemessagesspanspan-idcopyingtracemessagesspancopying-trace-messages"></a><span id="copying_trace_messages"></span><span id="COPYING_TRACE_MESSAGES"></span>复制跟踪消息

要复制跟踪消息从跟踪消息列表，请执行以下操作：

1.  选择你想要复制的跟踪消息。 可以使用 SHIFT + 单击选择连续消息或 CTRL + 单击以复制非连续的邮件。

2.  按 CTRL + C。 或者，右键单击的任何所选的跟踪任何的消息单元格，并单击**复制**。

这些消息将复制的制表符分隔格式。 可以将其粘贴到文本文件或电子表格文件以供将来使用。

有关保存跟踪消息的详细信息，请参阅[创建文本版本的跟踪日志](creating-text-versions-of-trace-logs.md)。

 

 





